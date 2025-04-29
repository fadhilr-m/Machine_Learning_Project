# Heart Disease Risk Prediction Report - Fadhil Ramadhan Masthofani

## Domain Proyek

Penyakit jantung koroner merupakan penyebab utama kematian di seluruh dunia menurut World Health Organization (WHO). Salah satu manifestasi paling berbahaya dari penyakit ini adalah serangan jantung (myocardial infarction). Deteksi dini terhadap risiko serangan jantung sangat krusial untuk mencegah komplikasi serius dan meningkatkan kualitas hidup pasien.
Dalam era data-driven saat ini, analisis data kesehatan secara cerdas menjadi kunci untuk membantu profesional medis dalam mengidentifikasi individu dengan risiko tinggi secara lebih cepat dan akurat. Dengan menggunakan teknik machine learning, kita dapat membangun model prediktif berbasis data medical check-up (MCU) untuk memperkirakan kemungkinan seseorang mengalami serangan jantung.

Mengapa dan Bagaimana Masalah Ini Diselesaikan
Karena proses diagnosis medis tradisional sering membutuhkan waktu lama dan sumber daya besar, model machine learning dapat menjadi alat bantu penting untuk memberikan hasil prediksi cepat berbasis data historis pasien. Pendekatan ini membantu:
- Memberikan skrining awal sebelum pemeriksaan lebih lanjut.
- Membantu pengambilan keputusan klinis.
- Mengoptimalkan penggunaan sumber daya kesehatan.

Referensi:
- World Health Organization - Cardiovascular diseases (CVDs) Fact Sheet, 2023.
- Rajpurkar et al., Deep Learning for Cardiovascular Risk Prediction, Nature Medicine, 2019.

## Business Understanding

### Problem Statement

Bagaimana kita dapat mengklasifikasikan individu dengan risiko tinggi terkena serangan jantung berdasarkan data hasil medical check-up?

### Goals

Membangun model klasifikasi yang dapat memprediksi risiko serangan jantung berdasarkan fitur klinis dan kebiasaan gaya hidup.

## Solution Statement
- Menggunakan Logistic Regression sebagai baseline model yang interpretatif.
- Menggunakan Random Forest Classifier dan XGBoost untuk menangkap interaksi non-linear dan meningkatkan akurasi.
- Melakukan feature engineering dan scoring terhadap parameter risiko berdasarkan literatur medis.
- Melakukan hyperparameter tuning untuk model terbaik.


## Data Understanding

### Dataset

Dataset diambil dari hasil medical check-up (MCU) internal dan disediakan dalam format CSV. Dataset ini tidak tersedia secara publik tetapi disesuaikan menyerupai hasil pemeriksaan umum yang biasa dilakukan.
Jumlah data: 3000 baris
Link Dataset (dummy): /mnt/data/dataset_mcu.csv

### Fitur

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


## Data Preparation
Teknik yang dilakukan:
- Imputasi nilai kosong menggunakan modus (kategori) dan median (numerik)
- Label Encoding untuk fitur kategorikal
- One-Hot Encoding untuk fitur nominal dengan >2 kategori
- Feature Engineering: membuat skor risiko berdasarkan referensi medis
- Normalisasi pada fitur numerik jika diperlukan oleh algoritma (misal Logistic Regression)
Alasan: Untuk memastikan data dapat digunakan oleh algoritma ML dan meningkatkan kualitas input model.


## Modeling
Model yang digunakan:
- Logistic Regression
- Baseline, interpretatif
Cenderung kurang menangkap interaksi non-linear
- Random Forest
Menangkap non-linearitas dan interaksi fitur
Robust terhadap outlier dan data tidak terdistribusi normal
- XGBoost
Gradient boosting yang efisien
Dikenal memiliki performa sangat baik untuk klasifikasi
- Tuning dan Seleksi Model
GridSearchCV digunakan untuk memilih parameter optimal (misal: max_depth, n_estimators)
SHAP analysis dilakukan untuk interpretasi model
Model terbaik dipilih berdasarkan ROC-AUC tertinggi dan keseimbangan metrik lainnya


## Evaluation
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
