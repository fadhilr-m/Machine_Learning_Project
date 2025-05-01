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

   Risk Score tersebut diambil berdasarkan referensi jurnal
   

## Modeling

1. Logistic Regression:

  - Logistic Regression adalah model paling dasar dan paling mudah dipahami. Meskipun mungkin tidak memiliki performa terbaik, model ini sangat baik untuk baseline—menilai apakah model yang lebih kompleks dapat memberikan peningkatan yang signifikan dalam kinerja.
  - Logistic Regression bekerja baik ketika hubungan antar fitur bersifat linear, yang mungkin relevan untuk beberapa kasus medis sederhana di mana risiko didasarkan pada hubungan yang jelas antara fitur dan hasil.
  - Model ini sering digunakan dalam aplikasi dunia nyata di mana kecepatan interpretasi penting.

2. Random Forest:

  - Random Forest adalah model ensemble yang dapat menangani hubungan non-linear dan beragam jenis data. Model ini sangat baik dalam mengurangi overfitting, terutama saat berhadapan dengan data yang kompleks atau berisik.
  - Meskipun lebih sulit dipahami daripada Logistic Regression, RF memberikan hasil yang lebih stabil dan dapat dijelaskan sebagian melalui fitur penting yang diidentifikasi (misalnya, melalui feature importance).
  - Random Forest sering kali memberikan hasil yang sangat baik di berbagai tugas klasifikasi dan regresi tanpa memerlukan banyak pengaturan atau tunning hyperparameter.

3. XGBoost:

  - XGBoost adalah model ensemble yang berbasis pada gradient boosting dan sangat terkenal karena kemampuannya untuk memberikan hasil yang sangat akurat dalam waktu relatif singkat. Model ini bekerja baik untuk menangani data yang imbalanced, seperti dalam prediksi risiko medis.
  - XGBoost unggul dalam menangani data dengan hubungan non-linear yang kompleks. Dengan berbagai teknik untuk menangani overfitting (seperti regularisasi), XGBoost sering kali menghasilkan model dengan performansi terbaik di kompetisi data science.
  - Keunggulannya adalah kemampuan tuning hyperparameter yang sangat baik, memungkinkan model ini untuk beradaptasi dengan baik pada dataset yang beragam

4. Neural Network

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
| Logistic Regression |	0.65 | 0.58 | 0.54 | 0.55 |
| Random Forest	| 0.88 | 0.91 | 0.77 | 0.81 |
| XGBoost | 0.95 | 0.94 | 0.90 | 0.92 |
| Neural Network | 0.97 | 0.94 | 0.95 | 0.94 |

1. Accuracy

    - Logistic Regression (0.65): Hanya 65% prediksi total yang benar, menunjukkan model ini kurang mampu menangkap pola risiko kompleks
    - Random Forest (0.88): 88% prediksi benar, lonjakan besar dari LR berkat kemampuannya menangani non-linieritas
    - XGBoost (0.95): 95% benar—menunjukkan boostrap gradient sangat efektif
    - Neural Network (0.97): 97% benar, nilai tertinggi, model “menghafal” pola dengan sangat baik

2. Precision

    - Logistic Regression (0.58): Dari pasien yang diprediksi “berisiko”, hanya 58% benar-benar berisiko → banyak false positives
    - Random Forest (0.91): 91% prediksi positif tepat → false positives sangat sedikit
    - XGBoost (0.94) & Neural Network (0.94): Keduanya sangat andal dalam memprediksi risk-positives dengan kesalahan minimal

    Precision tinggi (RF, XGB, NN) berarti hampir tidak ada pasien sehat yang “dinyatakan berisiko” secara keliru.

3. Recall

    - Logistic Regression (0.54): Hanya mendeteksi 54% pasien berisiko → 46% “terlewat” (false negatives)
    - Random Forest (0.77): Menangkap 77% risiko → lebih baik tapi masih ada 23% yang lolos
    - XGBoost (0.90): Deteksi 90% pasien berisiko → kesalahan false negatives jauh berkurang
    - Neural Network (0.95): Deteksi 95% risiko → paling sedikit pasien berisiko yang terlewat

    NN dan XGB unggul karena meminimalkan risiko terlewat.

4. F1-Score

    - Logistic Regression (0.55): Harmonik precision & recall rendah → performa tidak seimbang
    - Random Forest (0.81): Keseimbangan cukup, didorong precision tinggi
    - XGBoost (0.92): Balance precision & recall sangat baik
    - Neural Network (0.94): Balance terbaik, menegaskan keunggulan komprehensif

    F1-Score tinggi (NN, XGB) menunjukkan model tidak hanya akurat, tetapi juga seimbang antara menghindari false positives dan false negatives.


Kesimpulan

  - Neural Network: Kombinasi accuracy tertinggi (0.97), precision tinggi (0.94), recall unggul (0.95), dan F1-Score terbaik (0.94) menjadikannya model paling andal untuk memprediksi risiko serangan jantung—terutama bila tujuan utama adalah menangkap sebanyak mungkin pasien berisiko tanpa terlalu banyak alarm palsu.
  - XGBoost: Nyaris setara NN (accuracy 0.95, F1-Score 0.92) dan juga pilihan sangat baik jika sumber daya komputasi atau interpretabilitas sedikit lebih dibutuhkan.
  - Random Forest: Precision sangat tinggi (0.91), cocok bila false positives harus diminimalkan, tetapi recall-nya (0.77) masih di bawah XGBoost/NN.
  - Logistic Regression: Cocok untuk baseline sederhana dan analisis cepat, namun kinerjanya paling rendah di semua metrik—kurang cocok untuk prediksi risiko medis yang serius.


Saran Pengembangan

- Validasi model menggunakan data Medical Check-Up (MCU) riil dari institusi kesehatan untuk meningkatkan akurasi dan relevansi klinis.
- Deploy model dalam bentuk aplikasi web interaktif agar dapat digunakan oleh pengguna umum atau tenaga medis.
- Tambahkan fitur gaya hidup seperti aktivitas fisik, pola makan, dan tingkat stres untuk memperkaya konteks prediksi.
- Gunakan data longitudinal (MCU tahunan) agar model dapat mendeteksi tren kesehatan individu secara lebih akurat.
- Kustomisasi model berdasarkan usia dan gender untuk meningkatkan presisi dan fairness.
- Evaluasi model dengan metrik cost-sensitive dan simulasi biaya salah prediksi untuk pengambilan keputusan medis.
- Libatkan dokter spesialis untuk menguji dan memvalidasi hasil model dalam konteks klinis nyata.
- Tambahkan fitur rekomendasi preventif otomatis berdasarkan hasil prediksi untuk mendorong tindakan nyata dari pengguna.

  
Referensi:

- World Health Organization. (2023). Cardiovascular Diseases (CVDs). [Online]. Tersedia: https://www.who.int
- Rajpurkar, P. et al. (2019). Deep Learning for Cardiovascular Risk Prediction. Nature Medicine. DOI:10.1038/s41591-019-0647-4
- D’Agostino, R. B., et al. (2008). “General Cardiovascular Risk Profile for Use in Primary Care: The Framingham Heart Study.” Circulation, 117(6), 743–753. Dasar pengembangan risk score klinis untuk memperkirakan kejadian kardiovaskular dalam 10 tahun ke depan.
- Goff, D. C., et al. (2014). “2013 ACC/AHA Guideline on the Assessment of Cardiovascular Risk.” Journal of the American College of Cardiology, 63(25), 2935–2959. Panduan American College of Cardiology/American Heart Association tentang stratifikasi risiko kardiovaskular.
- World Health Organization. (2007). “Prevention of Cardiovascular Disease: Pocket Guidelines for Assessment and Management of Cardiovascular Risk.” Model sederhana WHO untuk risk scoring yang dapat diaplikasikan di berbagai setting klinis.
- Kuhn, M., & Johnson, K. (2013). Applied Predictive Modeling. Springer. Bab tentang data preprocessing (handling missing data, one-hot encoding, scaling) dan persiapan fitur untuk model.
- Pedregosa, F., et al. (2011). “Scikit‐learn: Machine Learning in Python.” Journal of Machine Learning Research, 12, 2825–2830. Dokumentasi teknik-teknik preprocessing dan encoding di scikit-learn.
- Agardh, E., et al. (2011). “Modeling risk factors for cardiovascular disease: A review of the isotonic and spline‐based methods.” Statistics in Medicine, 30(3), 341–353. Contoh penggunaan metode pemodelan non-linier untuk variabel klinis.
