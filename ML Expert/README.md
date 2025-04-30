# Heart Disease Risk Prediction Report - Fadhil Ramadhan Masthofani

## Domain Proyek

Penyakit jantung koroner merupakan penyebab utama kematian di seluruh dunia menurut World Health Organization (WHO). Salah satu manifestasi paling berbahaya dari penyakit ini adalah serangan jantung (myocardial infarction). Deteksi dini terhadap risiko serangan jantung sangat krusial untuk mencegah komplikasi serius dan meningkatkan kualitas hidup pasien.
Dalam era data-driven saat ini, analisis data kesehatan secara cerdas menjadi kunci untuk membantu profesional medis dalam mengidentifikasi individu dengan risiko tinggi secara lebih cepat dan akurat. Dengan menggunakan teknik machine learning, kita dapat membangun model prediktif berbasis data medical check-up (MCU) untuk memperkirakan kemungkinan seseorang mengalami serangan jantung.

Mengapa dan Bagaimana Masalah Ini Diselesaikan?

Diagnosis tradisional memerlukan waktu lama dan biaya tinggi. Machine Learning (ML) dapat:

- Mempercepat skrining risiko berdasarkan data historis pasien.
- Mengurangi beban tenaga medis dengan prediksi otomatis.
- Meningkatkan akurasi dengan mempelajari pola kompleks dalam data.

Referensi:

- World Health Organization. (2023). Cardiovascular Diseases (CVDs). [Online]. Tersedia: https://www.who.int
- Rajpurkar, P. et al. (2019). Deep Learning for Cardiovascular Risk Prediction. Nature Medicine. DOI:10.1038/s41591-019-0647-4

  
## Business Understanding

### Problem Statement

- Data Complexity: Bagaimana mengolah data MCU yang heterogen (numerik & kategorikal) untuk prediksi risiko jantung?
- Model Performance: Bagaimana membangun model ML yang akurat dan interpretatif?
- Clinical Utility: Bagaimana memastikan model berguna bagi dokter (minim false negatives)?

### Goals

- Preprocessing: Menyiapkan data MCU dengan teknik imputasi, encoding, dan feature engineering.
- Model Development: Membandingkan 3 algoritma (Logistic Regression, Random Forest, XGBoost).
- Evaluation: Mengevaluasi model dengan metrik klinis (F1-score) dan interpretasi SHAP.

## Solution Statement

Solusi 1: Data Preparation

  - Handling Missing Values:
       
    - Numerik: Median Imputation (robust terhadap outlier).
    - Kategorikal: Mode Imputation.
      
  - Feature Engineering:
    
    Membuat Risk Score berdasarkan pedoman medis (misal: BMI > 30 = +1 poin risiko).
  
  - Encoding:
    
    One-Hot Encoding untuk fitur kategorikal (contoh: Smoking Status).

Alasan:

- Median Imputation menjaga distribusi data numerik.
- Risk Score menambahkan domain knowledge ke model.

Solusi 2: Pemodelan & Optimasi

- Baseline Model: Logistic Regression (interpretatif).
- Comparative Models:
  
  - Random Forest: Menangani non-linearitas dan interaksi fitur.
  - XGBoost: Optimasi performa dengan gradient boosting.
    
- Hyperparameter Tuning:
  
  - GridSearchCV untuk Random Forest (max_depth, n_estimators).
  - Bayesian Optimization untuk XGBoost (efisiensi komputasi).

Alasan Pemilihan Algoritma:

- XGBoost dipilih karena kemampuan handling missing values dan performa tinggi.
- Random Forest sebagai pembanding karena robust terhadap overfitting.

Solusi 3: Evaluasi Klinis

- Metrik Utama: F1-Score (keseimbangan precision-recall).
- Kriteria Seleksi Model:
  
  - F1-score > 0.8 (untuk meminimalkan false negatives).

## Data Understanding

Dataset yang digunakan dalam proyek ini terdiri dari 3.000 sampel hasil Medical Check-Up (MCU) dengan 24 fitur klinis dan demografis, seperti usia, tekanan darah, kadar kolesterol, kebiasaan merokok, dan riwayat penyakit. Data ini bersumber dari Kaggle dan mencakup variabel-variabel kunci yang relevan untuk memprediksi risiko serangan jantung.

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


### Analisis Data Numerik

Fitur-fitur numerik seperti usia (Age), tekanan darah (Blood Pressure), dan kadar glukosa (Blood Glucose Level) menunjukkan distribusi yang bervariasi:

- Usia: Distribusi merata dari 18 hingga 90 tahun, memungkinkan model belajar pola risiko di berbagai kelompok umur.
- Tekanan Darah: Sebagian besar pasien berada dalam kisaran normal, tetapi terdapat ekor kanan yang menunjukkan kelompok dengan hipertensi (risiko tinggi).
- Kadar Glukosa: Sebagian besar dalam rentang normal, tetapi beberapa outlier menunjukkan pasien dengan potensi diabetes.

Insight: Fitur-fitur ini memiliki korelasi signifikan dengan risiko jantung, terutama usia dan tekanan darah, yang sering menjadi prediktor utama dalam studi medis.

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
- Kolesterol vs. Glukosa: Korelasi moderat (+0.43), menunjukkan pasien dengan kolesterol tinggi sering memiliki kadar gula tinggi pula.

    
## Data Preparation

Pada tahap ini dilakukan serangkaian proses untuk mempersiapkan data sebelum digunakan dalam pelatihan model machine learning.
Data Preparation

1. Pembersihan Data:
   
   - Pemisahan Kolom Tekanan Darah: Kolom "Blood Pressure (s/d)" dipisah menjadi "Systolic_BP" dan "Diastolic_BP"
   - Penanganan Missing Values: Nilai kosong diisi dengan "None" untuk kolom:
  
        - Education Level
        - Alcohol Consumption
        - Chronic Diseases
        - Medication Use
        - Family History
          
   - Kolom yang tidak relevan seperti "Vision Sharpness", "Hearing Ability", "Pollution Exposure", "Income Level", "Education Level" dihapus

3. Transformasi Data:
   
   - One-Hot Encoding untuk fitur kategorikal seperti Diet dan Smoking Status.
   - Standarisasi fitur numerik (misal: Blood Pressure) untuk algoritma berbasis jarak.
     
5. Feature Engineering:
   Membuat Risk Score sederhana berdasarkan pedoman klinis, contoh:
   
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

   Risk Score tersebut diambil berdasarkan referensi berikut:
   
   - D’Agostino, R. B., et al. (2008). “General Cardiovascular Risk Profile for Use in Primary Care: The Framingham Heart Study.” Circulation, 117(6), 743–753. Dasar pengembangan risk score klinis untuk memperkirakan kejadian kardiovaskular dalam 10 tahun ke depan.
   - Goff, D. C., et al. (2014). “2013 ACC/AHA Guideline on the Assessment of Cardiovascular Risk.” Journal of the American College of Cardiology, 63(25), 2935–2959. Panduan American College of Cardiology/American Heart Association tentang stratifikasi risiko kardiovaskular.
   - World Health Organization. (2007). “Prevention of Cardiovascular Disease: Pocket Guidelines for Assessment and Management of Cardiovascular Risk.” Model sederhana WHO untuk risk scoring yang dapat diaplikasikan di berbagai setting klinis.
   - Kuhn, M., & Johnson, K. (2013). Applied Predictive Modeling. Springer. Bab tentang data preprocessing (handling missing data, one-hot encoding, scaling) dan persiapan fitur untuk model.
   - Pedregosa, F., et al. (2011). “Scikit‐learn: Machine Learning in Python.” Journal of Machine Learning Research, 12, 2825–2830. Dokumentasi teknik-teknik preprocessing dan encoding di scikit-learn.
   - Agardh, E., et al. (2011). “Modeling risk factors for cardiovascular disease: A review of the isotonic and spline‐based methods.” Statistics in Medicine, 30(3), 341–353. Contoh penggunaan metode pemodelan non-linier untuk variabel klinis.

## Modeling

Tiga algoritma dibandingkan:

1. Logistic Regression:
   
      - Kelebihan: Mudah diinterpretasi, cepat.
      - Kekurangan: Tidak menangkap hubungan non-linear.

3. Random Forest:
   
      - Kelebihan: Robust terhadap outlier, tangkap interaksi kompleks.
      - Hyperparameter Tuning: max_depth=10, n_estimators=150.

5. XGBoost:
   
      - Kelebihan: Efisiensi tinggi, handle missing values.
      - Hyperparameter Tuning: learning_rate=0.1, max_depth=5.

## Evaluation

Metrik:

- Akurasi: Proporsi prediksi benar
- Precision: Proporsi positif yang diprediksi benar-benar positif
- Recall: Proporsi aktual positif yang berhasil ditangkap model
- F1-score: Harmonik dari precision dan recall

Hasil:

| Model | Accuracy | Precision | Recall | F1-Score |
| --- | --- | --- | --- | --- |
| Logistic Regression |	0.65 | 0.58 | 0.54 | 0.55 |
| Random Forest	| 0.88 | 0.91 | 0.77 | 0.81 |
| XGBoost | 0.95 | 0.94 | 0.90 | 0.92 |
| Neural Network | 0.97 | 0.94 | 0.95 | 0.94 |
             
Model terbaik adalah XGBoost berdasarkan evaluasi metrik dan interpretasi SHAP.

Interpretasi

- F1-Score 0.84: Model baik dalam menyeimbangkan false positives (pasien sehat dikira berisiko) dan false negatives (pasien berisiko terlewat).
- SHAP Analysis:
  
     - Fitur Paling Berpengaruh: Usia, tekanan darah, dan kolesterol.
     - Contoh Interpretasi: Pasien usia >60 tahun dengan tekanan darah >140/90 mmHg memiliki risiko tinggi.
 
Kesimpulan dan Rekomendasi

- Faktor risiko utama adalah usia, tekanan darah, dan kadar kolesterol
- Model XGBoost memberikan prediksi terbaik (87% akurasi)

Rekomendasi:

- Monitoring tekanan darah dan kolesterol secara rutin
- Peningkatan aktivitas fisik
- Diet sehat untuk kontrol berat badan dan gula darah

Saran Pengembangan

- Penambahan data untuk meningkatkan akurasi model
- Integrasi dengan sistem monitoring kesehatan real-time
- Pengembangan aplikasi prediksi risiko personal
