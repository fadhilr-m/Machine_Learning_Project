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

Berdasarkan latar belakang di atas, permasalahan yang diselesaikan dalam proyek ini adalah:
- Bagaimana mengolah data MCU untuk prediksi risiko serangan jantung?
- Bagaimana membangun model machine learning yang akurat dalam mengklasifikasikan risiko serangan jantung?
- Bagaimana mengevaluasi model untuk mendapatkan performa terbaik?

### Goals

- Mengolah dan mempersiapkan data MCU untuk kebutuhan pelatihan model.
- Membuat model klasifikasi machine learning untuk memprediksi risiko serangan jantung.
- Mengevaluasi kinerja model menggunakan metrik akurasi, precision, recall, dan f1-score.


## Solution Statement

- Melakukan pembersihan dan preprocessing data, seperti menangani missing values dan encoding fitur kategorikal.
- Menerapkan berbagai algoritma klasifikasi seperti K-Nearest Neighbours, Random Forest, Neural Network, dan XGBoost.
- Melakukan tuning hyperparameter pada model terbaik (XGBoost) menggunakan Bayesian Optimization untuk meningkatkan performa.
- Mengevaluasi hasil model dengan classification report dan confusion matrix.



## Data Understanding

Dataset diambil dari hasil medical check-up (MCU) internal dan disediakan dalam format CSV. Dataset ini tidak tersedia secara publik tetapi disesuaikan menyerupai hasil pemeriksaan umum yang biasa dilakukan.
Jumlah data: 3000 baris
Link Dataset (dummy): /mnt/data/dataset_mcu.csv

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

## Data Preparation

Pada tahap ini dilakukan serangkaian proses untuk mempersiapkan data sebelum digunakan dalam pelatihan model machine learning.
1. Handling Missing Values
   Dilakukan pengecekan terhadap missing values pada dataset. Fitur yang memiliki banyak missing value dihapus. Untuk fitur dengan missing value sedikit, dilakukan imputasi menggunakan metode:
   - Mean Imputation untuk data numerik (seperti kolesterol, gula darah).
   - Most Frequent Imputation untuk data kategorikal

  Kesimpulan Analisis Data Numerik dan Kategorik
  Berdasarkan univariate analysis—melihat distribusi setiap fitur numerik dan frekuensi tiap kategori pada fitur kategorikal—dapat ditarik beberapa poin penting berikut:

1. Fitur Numerik
Age (Usia)
Distribusi relatif merata di rentang 18–90 tahun.
Tidak ada skewness ekstrem, artinya sampel mewakili berbagai kelompok usia secara seimbang.

BMI
Hampir membentuk kurva normal dengan puncak di 24–26.
Mayoritas pasien berada dalam rentang berat badan normal–pra-obsitas, sehingga model dapat belajar pola risiko dari rentang BMI umum.

Bone Density
Menunjukkan bimodalitas (dua puncak sekitar 0.8 dan 1.2 g/cm²).
Menandakan adanya dua sub‐populasi (kepadatan rendah vs normal/tinggi) yang potensial berkaitan dengan risiko jantung.


Blood Glucose Level
Sekitar normal dengan sedikit skew kanan (beberapa nilai tinggi >150 mg/dL).
Pasien dengan hiperglikemia ringan hingga moderat dominan, memberi sinyal penting untuk screening risiko.

Tekanan Darah (Systolic & Diastolic)
Keduanya dekat kurva normal namun memiliki ekor kanan (nilai tinggi).
Nilai tekanan darah tinggi (>160/100 mm Hg) perlu menjadi perhatian khusus dalam model.


Stress Levels & Sun Exposure
Distribusi relatif flat (seragam) di seluruh rentang.
Variasi merata memudahkan model memahami korelasi stres dan paparan sinar matahari terhadap risiko jantung tanpa bias ke kelompok tertentu.


Implikasi untuk Modeling:
Semua fitur numerik sudah cukup “bersih”—tidak perlu transformasi besar (misal log) selain scaling—dan outlier moderat dapat ditangani baik oleh model berbasis pohon maupun algoritma berbasis jarak.

2. Fitur Kategorikal
Gender
Distribusi seimbang antara “Male” dan “Female”, memudahkan model menangkap perbedaan risiko berdasarkan jenis kelamin.


Smoking Status
Terdiri dari “Former”, “Current”, dan “Never”, dengan dominasi “Former”.
Memberi sinyal bahwa riwayat merokok (bukan hanya status saat ini) penting dipertimbangkan.


Sleep Patterns
Kategori “Normal” paling banyak, disusul “Insomnia” dan “Excessive”.
Gangguan tidur (insomnia/kelebihan tidur) cukup umum dan bisa berperan sebagai faktor risiko.


Diet
“Balanced” dominan, diikuti “High-fat”, “Low-carb”, dan “Vegetarian”.
Pola makan beragam, memungkinkan analisis dampak diet spesifik pada risiko.


Physical Activity Level
Kategori “Moderate” tertinggi, lalu “Low” dan “High”.
Aktivitas moderat sebagai mayoritas menunjukkan kesempatan untuk mengukur efek perbedaan tingkat aktivitas.


Alcohol Consumption
“None” paling banyak, kemudian “Occasional” dan “Frequent”.
Konsumsi alkohol yang teratur atau berlebih dapat diuji korelasinya dengan peningkatan risiko.


Mental Health Status
“Good” dan “Fair” lebih banyak, “Poor” dan “Excellent” lebih sedikit.
Kesehatan mental memengaruhi stres dan faktor fisiologis lain—siap dianalisis lebih lanjut.


Chronic Diseases
Sebagian besar tanpa penyakit kronis, sisanya tersebar pada “Hypertension”, “Diabetes”, dan “Heart Disease”.
Kehadiran penyakit kronis jelas menjadi variabel kunci dalam memprediksi risiko jantung.


Medication Use
“None” paling tinggi, lalu “Regular” dan “Occasional”.
Pola konsumsi obat-obatan memberi indikasi status kesehatan dan pengelolaan penyakit.


Family History
Mayoritas “None”, sisanya “Diabetes”, “Hypertension”, “Heart Disease”.
Riwayat keluarga merupakan faktor genetik yang penting untuk model prediksi risiko.


Implikasi untuk Modeling:
Kategori-kategori ini harus di-encode (one-hot) agar model dapat menangkap perbedaan antar kelompok. Fitur seperti chronic diseases dan family history diharapkan memiliki bobot penting tinggi dalam prediksi karena hubungan genetik dan komorbiditas.

3. Kesimpulan Umum
Kelengkapan Data: Tidak ada fitur numerik dengan missing value signifikan; kategori “None” pada fitur kategorikal memastikan tidak ada data hilang yang diabaikan.

Variasi Fitur: Kombinasi distribusi normal, bimodal, dan seragam pada numerik, serta ragam kategori yang representatif, memberikan basis data yang kaya untuk model ML.
Kesiapan Preprocessing: Setelah imputasi sederhana, scaling numerik, dan encoding kategorikal, data siap dipakai untuk melatih berbagai model—terutama tree-based models (Random Forest, XGBoost) yang dapat menangkap pola non-linear dan interaksi antar fitur.
Univariate analysis ini memastikan kita memahami karakteristik dasar setiap fitur, meminimalkan risiko kesalahan preprocessing, dan memandu pilihan teknik modeling yang tepat.

Correlation map
Dari heatmap korelasi antar fitur numerik di atas, kita bisa mencermati beberapa poin penting:

Age vs Bone Density (−0.94)
Korelasi sangat kuat negatif: semakin tua usianya, umumnya kepadatan tulang (bone density) semakin rendah.
Implikasi: Karena ini hampir redundan, kita bisa mempertimbangkan hanya menyertakan salah satu di model linear, atau biarkan ensemble models (RF/XGBoost) menangkap pola ini secara otomatis.


Age vs Systolic_BP (0.65) & Age vs Diastolic_BP (0.61)
Korelasi positif sedang–kuat: tekanan darah (sistolik dan diastolik) cenderung naik seiring bertambahnya usia.
Implikasi: Usia dan tekanan darah saling berhubungan; di model yang peka multikolinearitas (misal regresi logistik), mungkin perlu memilih satu atau membuat fitur komposit (misal “age-adjusted BP”).


Bone Density vs Systolic_BP (−0.61) & Bone Density vs Diastolic_BP (−0.57)
Korelasi negatif sedang: pasien dengan tulang lebih padat cenderung memiliki tekanan darah lebih rendah.
Implikasi: Ini menegaskan pola “age → bone density → BP”; sekali lagi, tree-based models akan menangani interaksi ini dengan baik tanpa perlu penghapusan fitur.


Blood Glucose Level vs Age (0.43), Systolic_BP (0.27), Diastolic_BP (0.24)
Korelasi moderat positif dengan usia dan tekanan darah: pasien lebih tua dan dengan tekanan darah tinggi cenderung memiliki gula darah lebih tinggi.
Implikasi: Blood glucose memberikan sinyal tambahan di luar BP dan usia, layak dipertahankan sebagai prediktor independen.


Fitur Lainnya (BMI, Stress Levels, Sun Exposure)
Hampir semua korelasinya dekat nol dengan fitur lain, menandakan mereka membawa informasi unik.
Implikasi: BMI, stres, dan paparan sinar matahari akan membantu model menangkap dimensi risiko berbeda yang tidak terduga oleh usia/BP saja.


Rekomendasi untuk Pipeline selanjutnya
Tree-based models (Random Forest, XGBoost) akan otomatis memilih dan menggabungkan fitur‐fitur yang berkorelasi tanpa masalah multikolinearitas.


Kesimpulan dari analisis univariat dan korelasi ini memberikan gambaran yang lebih jelas tentang hubungan antar fitur yang ada dalam dataset. Beberapa poin penting yang dapat diambil adalah:

Usia dan Kepadatan Tulang: Terdapat korelasi negatif yang sangat kuat antara usia dan kepadatan tulang. Semakin tua usia seseorang, semakin rendah kepadatan tulangnya. Hal ini mengindikasikan bahwa faktor usia menjadi prediktor yang sangat penting dalam memahami kesehatan tulang.


Usia dan Tekanan Darah: Terdapat korelasi positif yang signifikan antara usia dan tekanan darah (baik sistolik maupun diastolik), yang berarti seiring bertambahnya usia, tekanan darah cenderung meningkat. Ini juga menunjukkan bahwa usia dan tekanan darah memiliki hubungan yang kuat, sehingga bisa dipertimbangkan sebagai faktor prediktif risiko serangan jantung.


Kepadatan Tulang dan Tekanan Darah: Korelasi negatif antara kepadatan tulang dan tekanan darah mengindikasikan bahwa individu dengan kepadatan tulang lebih tinggi mungkin memiliki tekanan darah yang lebih rendah. Hal ini bisa memberikan wawasan lebih lanjut dalam memahami pola kesehatan secara keseluruhan.


Glukosa Darah dan Faktor Lain: Glukosa darah menunjukkan korelasi positif moderat dengan usia dan tekanan darah, yang mengindikasikan bahwa individu yang lebih tua dan memiliki tekanan darah tinggi mungkin memiliki kadar glukosa yang lebih tinggi. Ini menunjukkan pentingnya faktor glukosa sebagai indikator tambahan dalam risiko serangan jantung.


Fitur Lain (BMI, Stress, Sun Exposure): Beberapa fitur lain seperti BMI, tingkat stres, dan paparan sinar matahari menunjukkan korelasi yang lebih rendah dengan fitur lain, yang berarti bahwa mereka dapat memberikan informasi yang lebih unik dan tidak bergantung pada faktor-faktor utama seperti usia atau tekanan darah.


Teknik yang dilakukan:
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
