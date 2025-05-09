# Heart Disease Risk Prediction Report - Fadhil Ramadhan Masthofani

## Domain Proyek

Penyakit jantung koroner merupakan penyebab utama kematian di seluruh dunia menurut World Health Organization (WHO). Salah satu manifestasi paling berbahaya dari penyakit ini adalah serangan jantung (myocardial infarction). Deteksi dini terhadap risiko serangan jantung sangat krusial untuk mencegah komplikasi serius dan meningkatkan kualitas hidup pasien.
Dalam era data-driven saat ini, analisis data kesehatan secara cerdas menjadi kunci untuk membantu profesional medis dalam mengidentifikasi individu dengan risiko tinggi secara lebih cepat dan akurat. Dengan menggunakan teknik machine learning, kita dapat membangun model prediktif berbasis data medical check-up (MCU) untuk memperkirakan kemungkinan seseorang mengalami serangan jantung.

Mengapa dan Bagaimana Masalah Ini Diselesaikan?

Diagnosis tradisional memerlukan waktu lama dan biaya tinggi. Machine Learning (ML) dapat:

- Mempercepat skrining risiko berdasarkan data historis pasien.
- Mengurangi beban tenaga medis dengan prediksi otomatis.
- Meningkatkan akurasi dengan mempelajari pola kompleks dalam data.

## Business Understanding

### Problem Statement

- Data Complexity: Bagaimana mengolah data MCU yang heterogen (numerik & kategorikal) untuk prediksi risiko jantung?
- Model Performance: Bagaimana membangun model ML yang akurat dan interpretatif?
- Clinical Utility: Bagaimana memastikan model berguna bagi dokter (minim false negatives)?

### Goals

- Preprocessing: Menyiapkan data MCU dengan teknik imputasi, encoding, dan feature engineering.
- Model Development: Membandingkan 3 algoritma (Logistic Regression, Random Forest, XGBoost).
- Evaluation: Mengevaluasi model dengan metrik klinis (F1-score).

## Solution Statement

Solusi 1: Data Preparation
      
  - Membuat Risk Score berdasarkan pedoman medis (misal: BMI > 30 = +1 poin risiko).
  
  - One-Hot Encoding untuk fitur kategorikal (contoh: Smoking Status).

Solusi 2: Pemodelan

  - Baseline Model: Logistic Regression (interpretatif).

  - Comparative Models antara Random Forest, XGBoost, dan Neural Network
  

Solusi 3: Evaluasi Klinis

  - Metrik Utama: F1-Score (keseimbangan precision-recall) > 0.8 (untuk meminimalkan false negatives).

## Data Understanding

Dataset yang digunakan dalam proyek ini terdiri dari 3.000 sampel hasil Medical Check-Up (MCU) dengan 26 fitur klinis dan demografis, seperti usia, tekanan darah, kadar kolesterol, kebiasaan merokok, dan riwayat penyakit. Data ini bersumber dari Kaggle dan mencakup variabel-variabel kunci yang relevan untuk memprediksi risiko serangan jantung. Berikut link yang dapat diakses

https://www.kaggle.com/datasets/abdullah0a/human-age-prediction-synthetic-dataset/data

Fiturnya adalah :
| Command | Description |
| --- | --- |
| Gender | Jenis kelamin |
| Height (cm) | Tinggi tubuh individu dalam satuan sentimeter |
| Weight (kg) | Berat tubuh individu dalam satuan kilogram |
| Blood Pressure (s/d) | Tekanan darah terukur, terdiri dari nilai sistolik dan diastolik dalam mmHg |
| Cholesterol Level (mg/dL) | Jumlah kolesterol dalam darah, diukur dalam miligram per desiliter |
| BMI | Rasio berat badan dan kuadrat tinggi badan, menunjukkan kategori berat tubuh |
| Blood Glucose Level (mg/dL) | Tingkat glukosa dalam darah, dicatat dalam miligram per desiliter |
| Bone Density (g/cm²) | Tingkat kepadatan tulang, diukur dalam gram per sentimeter persegi |
| Vision Sharpness | Penilaian ketajaman penglihatan pada skala 0 (sangat buram) hingga 100 (sangat tajam) |
| Hearing Ability (dB) |Tingkat pendengaran seseorang dalam desibel.
| Physical Activity Level | Kategori frekuensi aktivitas (rendah, sedang, atau tinggi) |
| Smoking Status | Kategori kebiasaan merokok (“Tidak Pernah”, “Pernah”, atau “Sedang Merokok”) |
| Alcohol Consumption | Frekuensi atau pola minum alkohol |
| Diet | Pola makan yang diikuti, misalnya “Seimbang”, “Tinggi Protein”, “Rendah Karbohidrat”, dll |
| Chronic Diseases | Adanya riwayat penyakit jangka panjang seperti diabetes atau hipertensi |
| Medication Use | Pola atau frekuensi pemakaian obat-obatan |
| Family History | Adakah riwayat penyakit terkait usia dalam keluarga (misalnya penyakit jantung) |
| Cognitive Function | Penilaian sendiri terhadap fungsi kognitif pada skala 0 (sangat buruk) hingga 100 (sangat baik) |
| Mental Health Status | Penilaian diri mengenai kesehatan mental pada skala 0 (buruk) hingga 100 (prima) |
| Sleep Patterns | Rata-rata jam tidur per malam |
| Stress Levels | Penilaian tingkat stres diri sendiri pada skala 0 (rendah) hingga 100 (tinggi) |
| Pollution Exposure | Tingkat paparan polutan lingkungan dalam satuan unit tak baku |
| Sun Exposure | Rata-rata jam paparan matahari per minggu |
| Education Level | Jenjang pendidikan tertinggi yang telah dicapai |
| Income Level | Pendapatan per tahun dalam dolar Amerika Serikat |
| Age (years) | usia individu dalam tahun |

## Exploratory Data Analysis

Pada tahap ini dilakukan serangkaian proses untuk mempersiapkan data sebelum digunakan dalam pelatihan model machine learning.
Data Preparation

1. Pembersihan Data:
   
   - Kolom yang tidak relevan seperti "Vision Sharpness", "Hearing Ability", "Pollution Exposure", "Income Level", "Education Level" dihapus

2. Transformasi Data:

   - Pemisahan Kolom Tekanan Darah: Kolom "Blood Pressure (s/d)" dipisah menjadi "Systolic_BP" dan "Diastolic_BP"
   - Penanganan Missing Values: Nilai kosong diisi dengan "None" untuk kolom:
  
        - Education Level
        - Alcohol Consumption
        - Chronic Diseases
        - Medication Use
        - Family History

### Analisis Data Numerik

- Sebagian besar fitur numerik memiliki distribusi mendekati normal, cocok untuk model klasik seperti logistic regression
- Fitur seperti Age, Stress Levels, dan Sun Exposure menunjukkan distribusi yang tidak normal (flat/uniform), yang artinya hubungan terhadap target mungkin tidak linier — model non-linier seperti tree-based (Random Forest, XGBoost) bisa lebih baik.
- Tidak ada outlier mencolok, semua fitur terdistribusi wajar — ini memudahkan training model tanpa transformasi agresif.
- Multikolinearitas kemungkinan rendah, mengingat distribusi yang cukup berbeda satu sama lain.

### Analisis Data Kategorikal

Fitur seperti kebiasaan merokok (Smoking Status), aktivitas fisik (Physical Activity Level), dan riwayat keluarga (Family History) memberikan konteks penting:

- Perokok Aktif/Mantan: 45% sampel memiliki riwayat merokok, yang secara klinis terkait dengan peningkatan risiko jantung.
- Aktivitas Fisik Rendah: 30% pasien termasuk kategori kurang aktif, yang dapat berkontribusi pada obesitas dan hipertensi.
- Riwayat Keluarga: Sekitar 20% memiliki keluarga dengan penyakit jantung, mengindikasikan faktor genetik.

Insight: Fitur-fitur ini membantu model memahami gaya hidup dan faktor risiko non-fisiologis.
Analisis Korelasi Antar Fitur

### Heatmap

Heatmap korelasi mengungkap hubungan menarik:

- Usia vs. Tekanan Darah: Korelasi positif (+0.65), artinya semakin tua, tekanan darah cenderung lebih tinggi.
- Usia vs. Kepadatan Tulang: Korelasi negatif kuat (-0.94), karena penuaan alami mengurangi kepadatan tulang.
- Usia vs. Glukosa: Korelasi moderat (+0.43), menunjukkan pasien dengan usia lanjut sering memiliki kadar gula tinggi pula.
- Usia vs. Kolesterol: Korelasi moderat (+0.43), menunjukkan pasien dengan usia lanjut sering memiliki kadar gula tinggi pula.

    
## Data Preparation
     
1. Membuat Risk Score sederhana berdasarkan pedoman klinis, contoh:
   
      - Usia (>55 tahun = 2 poin, 45-55 = 1 poin)
      - Tekanan darah (≥140/90 = 2 poin, ≥130/85 = 1 poin)
      - Kolesterol (≥240 = 2 poin, ≥200 = 1 poin)
      - Gula darah (≥126 = 2 poin, ≥110 = 1 poin)
      - BMI (≥30 = 2 poin, ≥25 = 1 poin)
      - Merokok (2 poin)
      - Aktivitas fisik rendah (1 poin)
      - Riwayat keluarga (2 poin)
        
   Kategori risiko:
   
   - Rendah: <4
   - Sedang: 4-7
   - Tinggi: ≥8
  
  Risk Score tersebut diambil berdasarkan referensi jurnal

  - One-Hot Encoding untuk fitur kategorikal seperti Diet dan Smoking Status.
  - Standarisasi fitur numerik (misal: Blood Pressure) untuk algoritma berbasis jarak.

2. One Hot Encoding

    Pada tahap ini, dilakukan One-Hot Encoding terhadap kolom-kolom kategorikal untuk mengubah nilai string menjadi bentuk numerik biner. Ini penting karena sebagian besar algoritma machine learning tidak dapat menangani data bertipe string secara langsung.

    Langkah-langkah yang dilakukan:

    - Inisialisasi encoder menggunakan OneHotEncoder dari Scikit-Learn dengan opsi handle_unknown='ignore', yang menghindari error jika ada kategori baru saat prediksi.
    - Melatih encoder dan sekaligus mentransformasi fitur kategorikal menjadi matriks sparse biner.
    - Mengubah hasil encoding menjadi array dan kemudian DataFrame, dengan nama kolom dihasilkan otomatis oleh get_feature_names_out().
    - Menggabungkan DataFrame hasil encoding dengan data awal, menghapus kolom kategorikal asli karena sudah diwakili oleh kolom hasil encoding.

    Hasil akhirnya adalah DataFrame df_analysis_encoded yang siap digunakan untuk modeling dengan semua fitur dalam bentuk numerik.

3. Splitting Data Train dan Data Validation

    Pada tahap ini, kita memisahkan data menjadi dua bagian:

    X (Fitur): Kolom yang digunakan untuk memprediksi risiko, dengan menghapus kolom target (heart_disease_risk_score dan heart_disease_risk_category).

    y (Target): Kolom yang berisi kategori risiko serangan jantung (heart_disease_risk_category).

   Pembagian dilakukan dengan proporsi 70% untuk data training dan 30% untuk data validation menggunakan train_test_split, dengan parameter stratify=y untuk memastikan distribusi target (y) tetap seimbang antara kedua subset.

4. Standarisasi

    Penggunaan StandardScaler dalam preprocessing data bertujuan untuk menstandarisasi fitur numerik agar memiliki rata-rata 0 dan standar deviasi 1. Ini penting karena banyak algoritma machine learning—seperti K-Nearest Neighbors (KNN), Regresi Logistik, SVM, dan bahkan Neural Network sensitif terhadap skala fitur Melakukan transformasi standarisasi pada kolom numerik, baik di data pelatihan maupun validasi

  Tujuan:
  - Menormalkan skala data untuk meningkatkan performa dan konvergensi model.
  - Agar tidak terjadi data leakage dari validation set.

## Modeling

1. Logistic Regression:

Logistic Regression adalah algoritma klasifikasi yang digunakan untuk memprediksi probabilitas suatu instance termasuk dalam kelas tertentu. Meskipun namanya mengandung "regression", ini adalah algoritma klasifikasi yang populer.

Cara kerjanya:

- Menggunakan fungsi sigmoid untuk memetakan output persamaan linier ke dalam range [0, 1]
- Fungsi sigmoid: σ(z) = 1 / (1 + e^(-z)), dimana z adalah kombinasi linier fitur input
- Output diinterpretasikan sebagai probabilitas kelas
- Threshold default 0.5 digunakan untuk menentukan prediksi kelas (jika probabilitas ≥ 0.5, prediksi kelas 1; jika < 0.5, prediksi kelas 0)

Pembahasan Parameter :

- max_iter=1000:
  
  Menentukan jumlah maksimum iterasi untuk optimizer konvergen
  
  Default biasanya 100 dan bida dinaikkan untuk memastikan konvergensi pada dataset yang lebih kompleks

- random_state=42:

  - Mengontrol random shuffling data
  - Digunakan untuk reproducibility hasil
  - Default=None (tidak di-set)
  - 42 adalah nilai arbitrer yang umum digunakan


  - Logistic Regression adalah model paling dasar dan paling mudah dipahami. Meskipun mungkin tidak memiliki performa terbaik, model ini sangat baik untuk baseline—menilai apakah model yang lebih kompleks dapat memberikan peningkatan yang signifikan dalam kinerja.
  - Logistic Regression bekerja baik ketika hubungan antar fitur bersifat linear, yang mungkin relevan untuk beberapa kasus medis sederhana di mana risiko didasarkan pada hubungan yang jelas antara fitur dan hasil.
  - Model ini sering digunakan dalam aplikasi dunia nyata di mana kecepatan interpretasi penting.

2. Random Forest:

Random Forest adalah algoritma ensemble learning yang menggunakan pendekatan "bagging" dengan membangun banyak decision tree dan menggabungkan hasilnya.

Cara kerjanya:

- Membuat banyak decision tree (disebut "forest") dengan:
- Bagging: Setiap tree dilatih pada subset data yang di-sampling dengan penggantian (bootstrap sample)
- Feature Randomness: Setiap split dalam tree hanya mempertimbangkan subset fitur yang dipilih secara acak

Untuk prediksi klasifikasi:

- Setiap tree memberikan "vote" untuk kelas tertentu
- Kelas dengan vote terbanyak menjadi prediksi akhir
- Mengurangi overfitting dengan averaging hasil dari banyak tree

Pembahasan Parameter

- n_estimators=100:
  - Jumlah tree dalam forest
  - Default=100
  - Nilai lebih tinggi biasanya meningkatkan performa tetapi meningkatkan waktu komputasi

- random_state=42:
  - Mengontrol randomness untuk reproducibility
  - Mengontrol bootstrap sampling dan seleksi fitur
  - Default=None (tidak di-set)

  - Random Forest adalah model ensemble yang dapat menangani hubungan non-linear dan beragam jenis data. Model ini sangat baik dalam mengurangi overfitting, terutama saat berhadapan dengan data yang kompleks atau berisik.
  - Meskipun lebih sulit dipahami daripada Logistic Regression, RF memberikan hasil yang lebih stabil dan dapat dijelaskan sebagian melalui fitur penting yang diidentifikasi (misalnya, melalui feature importance).
  - Random Forest sering kali memberikan hasil yang sangat baik di berbagai tugas klasifikasi dan regresi tanpa memerlukan banyak pengaturan atau tunning hyperparameter.

3. XGBoost:

XGBoost (Extreme Gradient Boosting) adalah algoritma ensemble learning berbasis boosting yang menggunakan gradient descent untuk meminimalkan loss function.

Cara kerjanya:

- Membangun decision trees secara sequential (berbeda dengan Random Forest yang parallel).
- Setiap tree baru mencoba mengoreksi kesalahan prediksi tree sebelumnya (boosting).
- Menggunakan gradient descent untuk mengoptimasi loss function (regresi: MSE, klasifikasi: log loss).
- Memanfaatkan regularisasi (L1/L2) untuk mencegah overfitting.
- Memiliki fitur built-in cross-validation dan dapat menangani missing values.

Pembahasan Parameter

- n_estimators=100

  - Jumlah decision trees yang dibangun.
  - Default = 100.
  - Nilai lebih tinggi meningkatkan akurasi tetapi berisiko overfitting.

- max_depth=6

  - Kedalaman maksimum setiap tree.
  - Default = 6.
  - Nilai tinggi → model lebih kompleks (risiko overfitting).

- learning_rate=0.1

  - Langkah pembelajaran (shrinkage) untuk mengontrol kontribusi setiap tree.
  - Default = 0.3.
  - Nilai kecil (e.g., 0.01) membuat model lebih lambat tetapi lebih presisi.

- random_state=42

  - Untuk reproducibility hasil.
  - Default = None (random).


  - XGBoost adalah model ensemble yang berbasis pada gradient boosting dan sangat terkenal karena kemampuannya untuk memberikan hasil yang sangat akurat dalam waktu relatif singkat. Model ini bekerja baik untuk menangani data yang imbalanced, seperti dalam prediksi risiko medis.
  - XGBoost unggul dalam menangani data dengan hubungan non-linear yang kompleks. Dengan berbagai teknik untuk menangani overfitting (seperti regularisasi), XGBoost sering kali menghasilkan model dengan performansi terbaik di kompetisi data science.
  - Keunggulannya adalah kemampuan tuning hyperparameter yang sangat baik, memungkinkan model ini untuk beradaptasi dengan baik pada dataset yang beragam

4. Neural Network

Cara Kerja Neural Network

Neural Network adalah model machine learning yang terinspirasi dari struktur biologis otak manusia. Model ini terdiri dari lapisan-lapisan (layers) yang saling terhubung:

- Input Layer: Menerima data fitur yang telah di-scale

- Hidden Layers: Melakukan transformasi non-linear pada data melalui:

  - Dense Layers: Setiap neuron terhubung penuh ke layer sebelumnya
  - Activation Functions: Menggunakan ReLU (Rectified Linear Unit) untuk non-linearitas
  - Dropout Layer: Untuk regularisasi dengan mematikan neuron secara acak

- Output Layer:

  - Menggunakan softmax untuk klasifikasi multi-kelas
  - Jumlah neuron sesuai dengan jumlah kelas target

Persiapan Data yang Mendukung Neural Network

(a) Feature Scaling

   - Neural Network sangat sensitif terhadap skala data.
   - Dengan Feature Scaling Ini membuat training lebih stabil dan konvergen lebih cepat.

(b) Label Encoding

   - Label kategori di-encode ke integer dengan LabelEncoder:
   - Format ini cocok untuk loss function sparse_categorical_crossentropy yang digunakan.

Arsitektur yang Dipilih

(a) Struktur Dasar

Input Layer:

Menyesuaikan dimensi fitur (shape=(X_train_scaled.shape[1],)).

Hidden Layers:

- 2 Dense Layers (64 dan 32 neuron) dengan aktivasi ReLU
- ReLU dipilih karena menghindari masalah vanishing gradient dan mempercepat training.
- Dropout = 0.5

Output Layer:

Menggunakan softmax untuk probabilitas multi-kelas.

(b) Optimasi dan Loss Function

- Optimizer: Adam (adaptif learning rate, cocok untuk kebanyakan kasus).
- Loss Function: sparse_categorical_crossentropy (efisien untuk label integer).

  - Neural Network sangat baik dalam mempelajari pola yang sangat kompleks di data besar. Model ini sangat berguna ketika hubungan antara fitur dan label tidak jelas atau linear.
  - Neural Networks dapat memberikan akurasi yang lebih baik, terutama ketika data memiliki banyak fitur atau sangat rumit. Meskipun kompleks dan memerlukan lebih banyak data, NN dapat memberikan hasil yang luar biasa di dataset besar dan variatif.
  - Neural Networks mampu bekerja dengan baik pada data yang tidak diolah atau tanpa banyak fitur rekayasa, berkat kemampuan mereka untuk mempelajari representasi yang baik dari data.


  Pemilihan Logistic Regression, Random Forest, XGBoost, dan Neural Network didasarkan pada kombinasi faktor-faktor berikut:

  - Sederhana tapi efektif (LR), cocok untuk baseline.
  - Tahan terhadap overfitting dan bisa mengelola data besar (RF, XGBoost, NN).
  - Kemampuan menangani data yang kompleks dan hubungan non-linear (XGBoost, NN).
  - Daya prediksi yang kuat dan akurasi tinggi, terutama untuk aplikasi kesehatan.

  Keempat model ini adalah representasi dari teknik yang beragam dalam pembelajaran mesin yang sudah terbukti efektif di berbagai aplikasi klasifikasi.



## Evaluation

Metrik:

1. Accuracy

    Accuracy adalah proporsi keseluruhan prediksi yang benar—baik positif maupun negatif. Metrik ini berguna saat kelas positif/negatif seimbang. Namun bisa menyesatkan bila data sangat tidak seimbang (misal: 99% negatif, model selalu prediksi negatif → akurasi 99% padahal recall positif = 0).

    Formula:

    ${Accuracy} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}​$

    TP (True Positive): jumlah kasus positif yang benar-benar diprediksi positif.

    TN (True Negative): jumlah kasus negatif yang benar-benar diprediksi negatif.

    FP (False Positive): jumlah kasus negatif yang salah diprediksi positif.

    FN (False Negative): jumlah kasus positif yang salah diprediksi negatif.


2. Precision

    Dari semua prediksi “positif” (berisiko), seberapa banyak yang benar-benar positif. Tujuannya adalah mengevaluasi keandalan model pada prediksi positif. Jika nilai Precision tinggi maka akan sedikit false positives. Namun jika nilai precision turun jika model banyak “berlebihan” menandai negatif sebagai positif.

    Formula:

    ${Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}$


3. Recall (Sensitivity)

    Dari semua kasus positif sebenarnya, seberapa banyak yang berhasil terdeteksi model. Tujuannya adalah mengevaluasi kemampuan model menangkap semua kasus positif. Jika nilai recall tinggi maka akan terjadi sedikit false negatives sehingga meminimalkan pasien berisiko yang tidak terdeteksi

    Formula:

    ${Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}$​


4. F1-Score

    F1-Score merupakan rata-rata antara precision dan recall. Lebih sensitif terhadap nilai rendah di salah satu metrik (karena memakai rata-rata harmonik). Hal ini akan berjalan optimal jika membutuhkan keseimbangan antara penghindaran false positives dan false negatives.

    Formula:

    ${F1-Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$


### Hasil:

| Model | Accuracy | Precision | Recall | F1-Score |
| --- | --- | --- | --- | --- |
| Logistic Regression |	0.85 | 0.83 | 0.83 | 0.83 |
| Random Forest	| 0.88 | 0.91 | 0.77 | 0.81 |
| XGBoost | 0.95 | 0.94 | 0.90 | 0.92 |
| Neural Network | 0.97 | 0.96 | 0.95 | 0.96 |

1. Accuracy

    - Logistic Regression (0.85): 85% prediksi total yang benar, menunjukkan model ini mampu menangkap pola risiko kompleks
    - Random Forest (0.88): 88% prediksi benar, tidak berbeda jauh dari Logreg dengan kemampuannya menangani non-linieritas
    - XGBoost (0.95): 95% benar—menunjukkan boostrap gradient sangat efektif
    - Neural Network (0.97): 97% benar, nilai tertinggi, model “menghafal” pola dengan sangat baik

2. Precision

    - Logistic Regression (0.83): Dari pasien yang diprediksi “berisiko”, 83% benar-benar berisiko → banyak false positives
    - Random Forest (0.91): 91% prediksi positif tepat → false positives sangat sedikit
    - XGBoost (0.94) & Neural Network (0.96): Keduanya sangat andal dalam memprediksi risk-positives dengan kesalahan minimal

    Precision tinggi (RF, XGB, NN) berarti hampir tidak ada pasien sehat yang “dinyatakan berisiko” secara keliru.

3. Recall

    - Logistic Regression (0.83): Hanya mendeteksi 83% pasien berisiko → 17% “terlewat” (false negatives)
    - Random Forest (0.77): Menangkap 77% risiko → lebih buruk dan masih ada 23% yang lolos
    - XGBoost (0.90): Deteksi 90% pasien berisiko → kesalahan false negatives jauh berkurang
    - Neural Network (0.95): Deteksi 95% risiko → paling sedikit pasien berisiko yang terlewat

    NN dan XGB unggul karena meminimalkan risiko terlewat.

4. F1-Score

    - Logistic Regression (0.83): Harmonik precision & recall rendah → performa seimbang
    - Random Forest (0.81): Keseimbangan cukup, didorong precision tinggi namun masih dibawah Logreg
    - XGBoost (0.92): Balance precision & recall sangat baik
    - Neural Network (0.96): Balance terbaik, menegaskan keunggulan komprehensif

    F1-Score tinggi (NN, XGB) menunjukkan model tidak hanya akurat, tetapi juga seimbang antara menghindari false positives dan false negatives.


Kesimpulan

- Model berhasil menangani data heterogen (numerik dan kategorikal) dengan baik. Teknik imputasi dan encoding yang digunakan memastikan data dapat diproses oleh model tanpa menambah bias. Proses ini sangat krusial dalam konteks medis, di mana kualitas data yang digunakan bisa mempengaruhi hasil prediksi secara signifikan. Solusi yang diterapkan memungkinkan model untuk tetap akurat meski data memiliki berbagai tipe dan sumber.
- Model yang dihasilkan sangat berguna bagi dokter karena dapat meminimalkan false negatives (pasien yang berisiko tapi tidak terdeteksi). Ini sangat penting dalam konteks medis untuk memastikan tindakan preventif dapat dilakukan dengan tepat waktu. Dengan akurasi yang tinggi dan interpretasi yang jelas (melalui metrik seperti precision, recall, dan F1-score), dokter dapat mengandalkan model ini untuk membantu keputusan klinis mereka tanpa terlalu banyak kekhawatiran tentang kesalahan prediksi yang signifikan.
- Dengan pendekatan yang terstruktur dalam preprocessing, pemodelan, dan evaluasi, model ini mampu memprediksi risiko serangan jantung dengan akurasi dan keseimbangan yang tinggi, sangat berguna untuk pengambilan keputusan medis yang lebih tepat.
Implementasi machine learning dalam prediksi risiko kesehatan memberikan keunggulan kompetitif pada institusi kesehatan, dengan meningkatkan akurasi prediksi dan menyediakan layanan yang lebih personal dan tepat waktu kepada pasien.


Saran Pengembangan

Mengingat hasil yang sangat baik dari model Neural Network dan XGBoost, langkah berikutnya adalah validasi model dengan data riil dan implementasi model dalam bentuk aplikasi interaktif untuk dokter dan pasien. Ini akan mengoptimalkan penggunaan model dalam praktik medis yang sesungguhnya.
  
Referensi:

- Rajpurkar, P., Irvin, J., Ball, (2019). Deep learning for cardiovascular risk prediction. Nature Medicine, 25(1), 67–74. https://doi.org/10.1038/s41591-019-0647-4
- D’Agostino, R. B., Vasan, R. S., Pencina, M. J.(2008). General cardiovascular risk profile for use in primary care: The Framingham Heart Study. Circulation, 117(6), 743–753. https://doi.org/10.1161/CIRCULATIONAHA.107.699579
- Goff, D. C., Lloyd-Jones, D. M., Bennett, G.(2014). 2013 ACC/AHA guideline on the assessment of cardiovascular risk. Journal of the American College of Cardiology, 63(25), 2935–2959. https://doi.org/10.1016/j.jacc.2013.11.005
- World Health Organization. (2007). Prevention of cardiovascular disease: Pocket guidelines for assessment and management of cardiovascular risk. Geneva: WHO Press.
- Kuhn, M., & Johnson, K. (2013). Applied predictive modeling. New York: Springer. https://doi.org/10.1007/978-1-4614-6849-3
- Pedregosa, F., Varoquaux, G., Gramfort, A.(2011). Scikit-learn: Machine learning in Python. Journal of Machine Learning Research, 12, 2825–2830.
- Agardh, E., Ahlbom, A., Andersson, T.(2011). Modeling risk factors for cardiovascular disease: A review of the isotonic and spline-based methods. Statistics in Medicine, 30(3), 341–353. https://doi.org/10.1002/sim.4110
