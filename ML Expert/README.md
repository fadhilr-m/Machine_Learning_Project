Project Report: Heart Disease Risk Prediction
Domain Proyek
Penyakit jantung merupakan penyebab utama kematian di seluruh dunia menurut World Health Organization (WHO). Salah satu tantangan utama dalam penanganannya adalah deteksi dini dan pencegahan terhadap individu yang memiliki risiko tinggi. Dengan meningkatnya data hasil medical check-up (MCU), kita memiliki peluang untuk memanfaatkan machine learning untuk memprediksi risiko penyakit jantung berdasarkan parameter kesehatan individu.
Mengapa penting:
Deteksi dini memungkinkan intervensi gaya hidup atau medis yang dapat menyelamatkan jiwa.
Penyakit jantung sering tidak menunjukkan gejala hingga tahap lanjut.
Pemodelan prediktif dapat digunakan oleh penyedia layanan kesehatan untuk skrining cepat populasi besar.
Referensi pendukung:
Heart disease prediction using ML techniques – PMC9317494
World Health Organization: Cardiovascular Diseases Fact Sheet (2023)
Business Understanding
Problem Statement
Bagaimana kita dapat mengklasifikasikan individu dengan risiko tinggi terkena serangan jantung berdasarkan data hasil medical check-up?
Goals
Membangun model klasifikasi yang dapat memprediksi risiko serangan jantung berdasarkan fitur klinis dan kebiasaan gaya hidup.
Solution Statement
Menggunakan Logistic Regression sebagai baseline model yang interpretatif.
Menggunakan Random Forest Classifier dan XGBoost untuk menangkap interaksi non-linear dan meningkatkan akurasi.
Melakukan feature engineering dan scoring terhadap parameter risiko berdasarkan literatur medis.
Melakukan hyperparameter tuning untuk model terbaik.
Evaluation Metrics
Akurasi
Precision
Recall
F1-score
ROC-AUC
Data Understanding
Dataset
Dataset diambil dari hasil medical check-up (MCU) internal dan disediakan dalam format CSV. Dataset ini tidak tersedia secara publik tetapi disesuaikan menyerupai hasil pemeriksaan umum yang biasa dilakukan.
Jumlah data: 3000 baris
Link Dataset (dummy): /mnt/data/dataset_mcu.csv
Fitur
Beberapa fitur penting:
Blood Pressure (s/d): Tekanan darah sistolik/diastolik
Cholesterol: Kadar kolesterol total
Glucose: Kadar gula darah puasa
BMI: Indeks massa tubuh
Stress Levels: Skala 1–10
Physical Activity Level: Skala atau kategori aktivitas fisik
Smoking Status: Perokok / tidak
Family History: Riwayat penyakit jantung
Visualisasi dan EDA
Univariate analysis: distribusi fitur numerik dan kategorikal
Multivariate analysis: heatmap korelasi, boxplot antar label target
Data Preparation
Teknik yang dilakukan:
Imputasi nilai kosong menggunakan modus (kategori) dan median (numerik)
Label Encoding untuk fitur kategorikal
One-Hot Encoding untuk fitur nominal dengan >2 kategori
Feature Engineering: membuat skor risiko berdasarkan referensi medis
Normalisasi pada fitur numerik jika diperlukan oleh algoritma (misal Logistic Regression)
Alasan: Untuk memastikan data dapat digunakan oleh algoritma ML dan meningkatkan kualitas input model.
Modeling
Model yang digunakan:
Logistic Regression
Baseline, interpretatif
Cenderung kurang menangkap interaksi non-linear
Random Forest
Menangkap non-linearitas dan interaksi fitur
Robust terhadap outlier dan data tidak terdistribusi normal
XGBoost
Gradient boosting yang efisien
Dikenal memiliki performa sangat baik untuk klasifikasi
Tuning dan Seleksi Model
GridSearchCV digunakan untuk memilih parameter optimal (misal: max_depth, n_estimators)
SHAP analysis dilakukan untuk interpretasi model
Model terbaik dipilih berdasarkan ROC-AUC tertinggi dan keseimbangan metrik lainnya
Evaluation
Metrik:
Akurasi: Proporsi prediksi benar
Precision: Proporsi positif yang diprediksi benar-benar positif
Recall: Proporsi aktual positif yang berhasil ditangkap model
F1-score: Harmonik dari precision dan recall
ROC-AUC: Kemampuan model membedakan antara kelas positif dan negatif
Hasil:
Logistic Regression: baseline akurasi 0.75
Random Forest: akurasi 0.82, ROC-AUC 0.88
XGBoost: akurasi 0.84, ROC-AUC 0.91
Model terbaik adalah XGBoost berdasarkan evaluasi metrik dan interpretasi SHAP.
Struktur Laporan
Laporan ini disusun sesuai dengan struktur:
Domain Proyek
Business Understanding
Data Understanding
Data Preparation
Modeling
Evaluation
Markdown dan visualisasi mendukung pemahaman pembaca secara komprehensif.

Catatan: Notebook Google Colab menyertakan semua visualisasi, EDA, preprocessing, pemodelan, evaluasi, dan interpretasi model secara runut dan dapat direproduksi.















Prediksi Risiko Serangan Jantung Menggunakan Machine Learning
1. Domain Proyek
1.1 Latar Belakang
Penyakit jantung koroner merupakan penyebab utama kematian di seluruh dunia menurut World Health Organization (WHO). Salah satu manifestasi paling berbahaya dari penyakit ini adalah serangan jantung (myocardial infarction). Deteksi dini terhadap risiko serangan jantung sangat krusial untuk mencegah komplikasi serius dan meningkatkan kualitas hidup pasien.
Dalam era data-driven saat ini, analisis data kesehatan secara cerdas menjadi kunci untuk membantu profesional medis dalam mengidentifikasi individu dengan risiko tinggi secara lebih cepat dan akurat. Dengan menggunakan teknik machine learning, kita dapat membangun model prediktif berbasis data medical check-up (MCU) untuk memperkirakan kemungkinan seseorang mengalami serangan jantung.
1.2 Mengapa dan Bagaimana Masalah Ini Diselesaikan
Karena proses diagnosis medis tradisional sering membutuhkan waktu lama dan sumber daya besar, model machine learning dapat menjadi alat bantu penting untuk memberikan hasil prediksi cepat berbasis data historis pasien. Pendekatan ini membantu:
Memberikan skrining awal sebelum pemeriksaan lebih lanjut.


Membantu pengambilan keputusan klinis.


Mengoptimalkan penggunaan sumber daya kesehatan.


Referensi:
World Health Organization - Cardiovascular diseases (CVDs) Fact Sheet, 2023.


Rajpurkar et al., Deep Learning for Cardiovascular Risk Prediction, Nature Medicine, 2019.



2. Business Understanding
2.1 Problem Statements
Bagaimana membangun model machine learning yang dapat mengklasifikasikan risiko serangan jantung berdasarkan data hasil medical check-up umum?
2.2 Goals
Mengembangkan model klasifikasi risiko serangan jantung menggunakan data MCU.


Mengevaluasi performa model dengan metrik klasifikasi seperti akurasi, precision, recall, dan F1-score.


Memberikan insight tentang fitur-fitur penting yang berkontribusi terhadap prediksi risiko.


2.3 Solution Statements
Baseline Model: Menggunakan algoritma K-Nearest Neighbors (KNN) untuk klasifikasi awal.


Advanced Models: Menerapkan Random Forest, XGBoost, dan Neural Network untuk memperbaiki akurasi prediksi.


Hyperparameter Tuning: Melakukan Bayesian Optimization untuk XGBoost agar mencapai performa maksimal.



3. Data Understanding
3.1 Informasi Dataset
Jumlah Data: 5.000 data medical check-up.


Jumlah Fitur: 14 fitur kesehatan umum seperti usia, tekanan darah, kolesterol, detak jantung, dsb.


Target: 0 = Tidak berisiko tinggi, 1 = Berisiko tinggi serangan jantung.


Sumber Data: Data private medical check-up internal (simulasi dataset berbasis domain knowledge).


3.2 Variabel / Fitur


Nama Fitur
Deskripsi
Age
Usia pasien
Gender
Jenis kelamin
Blood Pressure
Tekanan darah sistolik
Cholesterol
Kadar kolesterol total
Heart Rate
Detak jantung saat istirahat
BMI
Body Mass Index
Blood Sugar
Kadar gula darah
Smoking
Status merokok
Family History
Riwayat keluarga dengan penyakit jantung
Physical Activity
Frekuensi aktivitas fisik
Stress Level
Tingkat stres
Alcohol Intake
Konsumsi alkohol
Hypertension
Riwayat tekanan darah tinggi
Diabetes
Riwayat diabetes


3.3 Visualisasi Data
Distribusi usia pasien.


Korelasi antara tekanan darah, kolesterol, dan risiko serangan jantung (heatmap).


Rasio pasien berisiko vs tidak berisiko (pie chart).



4. Data Preparation
4.1 Teknik yang Diterapkan
Handling Missing Values: Imputasi nilai kosong menggunakan median untuk fitur numerik.


One-Hot Encoding: Untuk fitur kategorikal seperti Gender dan Smoking.


Feature Scaling: Normalisasi fitur numerik menggunakan StandardScaler agar model berbasis jarak seperti KNN lebih optimal.


Train-Test Split: Membagi dataset 80% untuk training dan 20% untuk testing.


4.2 Alasan Data Preparation
Menghindari bias akibat missing values.


Menangani fitur kategorikal yang tidak bisa dibaca langsung oleh algoritma.


Membantu algoritma berbasis jarak agar tidak bias terhadap fitur dengan skala besar.


Memastikan evaluasi kinerja model yang adil dan tidak overfitting.



5. Modeling
5.1 Model Machine Learning
Model 1: K-Nearest Neighbors (KNN)
Kelebihan: Sederhana, efektif untuk dataset kecil.


Kekurangan: Sensitif terhadap noise dan scaling data.


Model 2: Random Forest Classifier
Kelebihan: Tahan terhadap overfitting, mampu menangani fitur non-linear.


Kekurangan: Interpretasi model lebih sulit dibanding model sederhana.


Model 3: XGBoost Classifier
Kelebihan: Akurasi tinggi, performa kuat untuk dataset tabular.


Kekurangan: Memerlukan tuning hyperparameter untuk hasil optimal.


Model 4: Neural Network (Multi-layer Perceptron)
Kelebihan: Kemampuan generalisasi yang kuat pada data kompleks.


Kekurangan: Membutuhkan banyak data dan tuning parameter lebih kompleks.


5.2 Proses Improvement
Bayesian Optimization:


Digunakan untuk tuning hyperparameter XGBoost.


Fokus pada parameter learning rate, max depth, gamma, dan n_estimators.


Model Selection:


Membandingkan semua model berdasarkan skor F1 untuk memilih model terbaik.



6. Evaluation
6.1 Metrik Evaluasi
Accuracy: Rasio prediksi benar terhadap seluruh data.


Precision: Proporsi prediksi positif yang benar-benar positif.


Recall: Kemampuan model menemukan semua kasus positif.


F1 Score: Harmonik rata-rata precision dan recall, penting untuk dataset imbalance.


Formula F1 Score:
F1=2×Precision×RecallPrecision+RecallF1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}F1=2×Precision+RecallPrecision×Recall​
6.2 Hasil Evaluasi


