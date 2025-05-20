# LAPORAN PROYEK SISTEM REKOMENDASI ANIME


# 1. Project Overview

## Latar Belakang

Dalam era digital saat ini, konten hiburan seperti anime telah menjadi konsumsi global dengan ribuan judul tersedia secara daring. Namun, pengguna seringkali kesulitan menemukan anime yang sesuai dengan preferensi mereka, terutama di luar anime populer yang umum direkomendasikan. Dengan banyaknya pilihan, pengguna memerlukan sistem rekomendasi yang dapat menyarankan anime relevan sesuai selera mereka. Sistem rekomendasi yang baik dapat meningkatkan waktu tonton, kepuasan pengguna, dan loyalitas terhadap platform.


Sistem rekomendasi anime dirancang untuk membantu pengguna menemukan anime yang sesuai dengan preferensi mereka. Latar belakang proyek ini adalah banyaknya jumlah anime yang tersedia, sehingga pengguna kesulitan memilih anime yang relevan. Sistem ini menggunakan pendekatan hybrid, menggabungkan content-based filtering dan collaborative filtering, untuk memberikan rekomendasi yang lebih personal dan akurat.


Proyek ini penting karena:

- Meningkatkan pengalaman pengguna dengan mengurangi waktu pencarian.
- Memanfaatkan data rating dan metadata anime untuk rekomendasi yang lebih relevan.
- Dapat diaplikasikan di platform streaming seperti MyAnimeList atau Crunchyroll.


# 2. Business Understanding

## Problem Statements

- Pengguna kesulitan menemukan anime baru yang sesuai dengan preferensi mereka.
- Banyaknya pilihan anime membuat pengguna bingung menentukan tontonan berikutnya.
- Sistem rekomendasi yang ada belum optimal dalam mempertimbangkan preferensi pengguna dan kesamaan konten.

## Goals

- Membangun sistem rekomendasi yang mempertimbangkan genre, rating, dan preferensi pengguna.
- Memberikan rekomendasi yang personalized berdasarkan riwayat tontonan.
- Meningkatkan akurasi rekomendasi dengan menggabungkan content-based dan collaborative filtering.

## Solution Approach

- Content-Based Filtering: Merekomendasikan anime berdasarkan kemiripan genre, durasi, dan rating.
- Collaborative Filtering: Merekomendasikan anime berdasarkan rating pengguna lain dengan preferensi serupa.
- Hybrid Approach: Menggabungkan kedua metode untuk meningkatkan kualitas rekomendasi.


# 3. Data Understanding

Dataset yang digunakan berasal dari Kaggle - Anime Recommendation Database 2020. Dataset ini terdiri dari 4 file yaitu :

1. animelist.csv
   
    Dataset ini berisi daftar semua anime yang terdaftar oleh pengguna beserta skor, status menonton, dan jumlah episode yang telah ditonton. Berikut adalah rincian kolom yang ada pada dataset ini:

   - user_id: ID pengguna yang dihasilkan secara acak dan tidak dapat diidentifikasi.
   - anime_id: ID MyAnimeList dari anime (misalnya, 1).
   - watching_status: Status anime dalam daftar anime pengguna (misalnya, 2).
   - watched_episodes: Jumlah episode yang telah ditonton oleh pengguna.
   - rating: Rating yang diberikan oleh pengguna.

    Dataset yang digunakan sebanyak 1 juta baris data (dataset aslinya : 109 juta baris data) karena keterbatasan systemn RAM Google Colab.


2. rating_complete.csv
   
    Merupakan subset dari animelist.csv, yang hanya mempertimbangkan anime yang telah selesai ditonton oleh pengguna (watching_status == 2) dan diberikan skor (score != 0). Dataset ini mencakup:

   - 57 juta rating yang diberikan oleh pengguna,
   - 16.872 anime yang diberikan rating oleh 310.059 pengguna.

    Kolom yang ada di dataset ini adalah:
   
   - user_id: ID pengguna yang dihasilkan secara acak.
   - anime_id: ID MyAnimeList dari anime yang telah diberi rating oleh pengguna.
   - rating: Rating yang diberikan oleh pengguna untuk anime

3. anime.csv

    Dataset ini berisi informasi umum tentang 17.562 anime yang ada di MyAnimeList, seperti genre, studio, durasi, rating, dll. Beberapa kolom yang ada di dataset ini adalah:

    - MAL_ID: ID MyAnimeList dari anime (misalnya, 1).
    - Name: Nama lengkap anime.
    - Score: Skor rata-rata yang diberikan oleh semua pengguna MyAnimeList.
    - Genres: Daftar genre anime yang dipisahkan oleh koma (misalnya, Action, Adventure, Comedy, Drama, Sci-Fi, Space).
    - English name: Nama anime dalam bahasa Inggris.
    - Japanese name: Nama anime dalam bahasa Jepang.
    - Type: Jenis anime (misalnya, TV, movie, OVA).
    - Episodes: Jumlah episode anime (misalnya, 26).
    - Aired: Tanggal siaran anime (misalnya, Apr 3, 1998 to Apr 24, 1999).
    - Premiered: Musim anime mulai tayang (misalnya, Spring 1998).
    - Producers: Daftar produser anime.
    - Licensors: Daftar perusahaan yang memiliki lisensi untuk anime.
    - Studios: Daftar studio yang memproduksi anime.
    - Source: Sumber anime (misalnya, manga, novel, buku).
    - Duration: Durasi per episode (misalnya, 24 menit per episode).
    - Rating: Rating usia anime (misalnya, R - 17+ untuk kekerasan dan profanitas).
    - Ranked: Peringkat anime berdasarkan skor.
    - Popularity: Peringkat berdasarkan jumlah pengguna yang menambahkan anime ke daftar mereka.
    - Members: Jumlah anggota komunitas yang tergabung dalam grup anime ini.
    - Favorites: Jumlah pengguna yang menandai anime ini sebagai "favorit".
    - Watching: Jumlah pengguna yang sedang menonton anime.
    - Completed: Jumlah pengguna yang telah menyelesaikan anime.
    - On-Hold: Jumlah pengguna yang menunda anime.
    - Dropped: Jumlah pengguna yang menghentikan anime.
    - Plan to Watch: Jumlah pengguna yang berencana menonton anime ini.
    - Score-10: Jumlah pengguna yang memberikan skor 10.
    - Score-9: Jumlah pengguna yang memberikan skor 9.
    - Score-8: Jumlah pengguna yang memberikan skor 8.
    - Score-7: Jumlah pengguna yang memberikan skor 7.
    - Score-6: Jumlah pengguna yang memberikan skor 6.
    - Score-5: Jumlah pengguna yang memberikan skor 5.
    - Score-4: Jumlah pengguna yang memberikan skor 4.
    - Score-3: Jumlah pengguna yang memberikan skor 3.
    - Score-2: Jumlah pengguna yang memberikan skor 2.
    - Score-1: Jumlah pengguna yang memberikan skor 1.

Variabel/Fitur Penting

- Fitur Konten: Genres, Score, duration_min, Type
- Fitur Interaksi Pengguna: user_id, anime_id, rating, watching_status

## Insight dari masing-masing dataset

### Insight Dataset anime.csv

- Terdapat lonjakan besar di tengah — kemungkinan besar pada skor 6 atau 7, yang umum terjadi pada banyak dataset rating pengguna.
- Sebagian besar anime memiliki jumlah episode <50
- Mayoritas anime ditujukan untuk remaja (PG-13) dan semua umur (G)
- Konten dewasa seperti Rx - Hentai, R+, dan R - 17+ masih cukup signifikan jumlahnya.
- Ada proporsi kecil dengan Unknown.
- Genre paling populer dalam industri anime didominasi oleh Comedy, diikuti oleh Action dan Fantasy, yang menunjukkan preferensi kuat audiens terhadap hiburan ringan dan petualangan. Genre seperti Drama, Slice of Life, dan Romance juga tetap relevan, menandakan variasi kebutuhan emosional dalam konsumsi konten anime.

### Insight dari rating.csv

- Mayoritas rating berada di rentang nilai 6 hingga 10, dengan puncak tertinggi pada rating 8.

### Insgiht dari dataset animelist_df

- Sebagian besar pengguna dalam dataset telah menyelesaikan anime, diikuti oleh sejumlah besar yang berencana untuk menonton, sementara proporsi pengguna yang sedang menonton, berhenti menonton, atau menunda menonton relatif kecil.
- Distribusi jumlah episode yang ditonton sangat condong ke kiri, dengan sebagian besar interaksi terjadi pada jumlah episode yang sangat sedikit, sementara hanya sebagian kecil interaksi yang melibatkan jumlah episode yang sangat banyak. Ini menunjukkan bahwa banyak pengguna mungkin baru memulai menonton anime atau belum menonton banyak episode dari anime yang ada dalam daftar mereka
- Anime dengan ID 1535 menjadi yang paling banyak berinteraksi dalam dataset, diikuti oleh variasi jumlah interaksi di antara sembilan anime teratas lainnya, dengan ID 20 dan 10620 menunjukkan jumlah interaksi yang relatif lebih rendah dalam kelompok ini.
- Pengguna dengan ID 20807 adalah yang paling aktif dalam dataset berdasarkan jumlah interaksi, diikuti oleh variasi tingkat aktivitas di antara sembilan pengguna teratas lainnya, dengan ID 4773, 6852, dan 18355 menunjukkan tingkat interaksi yang relatif lebih rendah dalam kelompok ini. Ini mengindikasikan adanya pengguna yang secara signifikan lebih terlibat dibandingkan dengan yang lain.
- Pengguna cenderung telah menonton lebih banyak episode pada anime yang masih mereka ikuti ("Watching") atau yang sudah mereka selesaikan ("Completed"). Sementara itu, anime yang ditunda ("On Hold") atau dihentikan ("Dropped") memiliki rata-rata episode yang ditonton lebih sedikit, dan anime yang baru direncanakan untuk ditonton ("Plan to Watch") memiliki rata-rata episode ditonton yang paling rendah.

Dikarenakan masih terdapat anomali pada anime_df seperti outlier, nilai 'Unknown', hingga durasi menit. maka akan dilakukan pembersihan data

# 4. 🧹 Data Preparation

Langkah-langkah Data Preparation

## 1. Pembersihan Data anime_df

### a. Membuat fungsi untuk membersihkan nilai pada kolom Score.

- Jika nilai adalah 'Unknown', maka diganti menjadi np.nan (Not a Number, atau nilai kosong).
- Jika nilai dapat dikonversi ke float, dikembalikan sebagai angka desimal.
- Jika gagal (karena format tidak sesuai), nilai juga dikembalikan sebagai np.nan.
- apply(clean_score) membersihkan setiap baris di kolom Score menggunakan fungsi di atas.
- Nilai kosong (NaN) setelah dibersihkan akan digantikan dengan nilai median dari kolom Score—langkah umum dalam imputasi data numerik agar distribusi tidak bias oleh outlier.
- Tujuannya adalah agar semua anime memiliki skor numerik yang valid.

  
### b. Membersihkan Kolom Genres

- Jika ada nilai kosong di kolom Genres, diisi dengan 'Unknown'.
- Koma diganti dengan spasi agar lebih mudah diproses dengan TF-IDF vectorizer (yang menganggap spasi sebagai pemisah antar kata). Misalnya: 'Action, Adventure' → 'Action Adventure'.

### c. Parsing Durasi Menit dari Kolom Duration

- Fungsi ini mengekstrak angka menit dari teks durasi, misalnya '24 min per ep' → 24.
- Jika tidak ada angka atau data kosong, hasilnya adalah 0.
- Hasil parsing ini disimpan ke kolom baru duration_min, yang akan berguna untuk filtering berdasarkan durasi (misalnya untuk rekomendasi saat makan siang).

Semua data sudah dilakukan pembersihan

## 2. Data Preprocessing

### a. Batasi dataset animelist.csv

karena animelist.csv memiliki 109 juta baris data, maka dibatasi hingga 10,000,0000 data saja karena keterbatasan dari RAM Google Colab.

### b. Menghitung Engagement Metrics

- Dataset animelist_df berisi interaksi user terhadap anime, seperti berapa episode yang ditonton (watched_episodes) dan status menontonnya (watching_status).
- groupby('anime_id') mengelompokkan data berdasarkan ID anime.
- avg_watched_episodes: rata-rata jumlah episode yang ditonton untuk tiap anime.
- completion_rate: persentase user yang menyelesaikan anime tersebut (watching_status == 2 biasanya berarti "Completed").

### c. Menggabungkan Engagement Metrics ke Dataset Anime

- Menggabungkan (merge) anime_df dengan engagement_stats berdasarkan ID anime.
- Jika ada anime yang tidak memiliki engagement data, nilainya diisi dengan 0 agar tetap bisa digunakan dalam modeling

### d. Menentukan Tingkat Engagement (Low, Medium, High)

- Membuat fitur baru engagement_level berdasarkan completion rate:

     > 0.7 → high
     > 0.4 → medium
     > Sisanya → low
     
Ini memberi kita indikator seberapa menarik atau mengikat suatu anime bagi penonton..

### e. Membuat Fitur Baru: enhanced_genres

- Menggabungkan teks genre asli dengan level engagement untuk menciptakan fitur enhanced_genres. Contoh: "Action Comedy" + "high" → "Action Comedy high"

### f. TF-IDF Vectorization terhadap Enhanced Genres

- TF-IDF (Term Frequency–Inverse Document Frequency) digunakan untuk mengubah teks genre (yang sudah diperkaya dengan engagement_level) menjadi representasi numerik.
- max_features=100: hanya mempertahankan 100 kata/term yang paling informatif dari genre.
- Output genre_tfidf berbentuk sparse matrix (matriks jarang) karena kebanyakan anime hanya memiliki sebagian kecil dari seluruh genre yang tersedia.

### g. Reduksi Dimensi dengan Truncated SVD

- TF-IDF menghasilkan ratusan dimensi sparse. Agar efisien untuk dihitung dan menghindari curse of dimensionality, digunakan SVD (Singular Value Decomposition).
- n_components=20: mereduksi representasi genre menjadi hanya 20 dimensi utama.


## 3. Normalisasi Data

### a. Normalisasi Fitur Numerik

Mengambil empat fitur numerik penting:

- Score: nilai rata-rata anime
- duration_min: durasi anime per episode (dalam menit)
- Members: jumlah anggota MyAnimeList yang menonton
- completion_rate: tingkat penyelesaian anime oleh pengguna
  
Digunakan MinMaxScaler untuk menskalakan semua nilai ke rentang [0, 1], sehingga adil untuk digunakan dalam model berbasis similarity (seperti cosine similarity).

### b. Menggabungkan Semua Fitur (Final Feature Matrix)

- Menggabungkan hasil TF-IDF genre (yang telah direduksi dimensinya) dengan fitur numerik yang telah dinormalisasi.
- hstack digunakan untuk menyusun matriks secara horizontal (menyatukan kolom).
- Digunakan csr_matrix untuk memastikan semua data tetap dalam format sparse demi efisiensi memori dan komputasi.


# Modeling 

### Similarity-based

Menghitung kemiripan antar anime berdasarkan fitur gabungan menggunakan cosine similarity. Ini adalah inti dari content-based recommendation.

#### a. Definisi Fungsi weighted_cosine_similarity()

Fungsi ini menghitung cosine similarity antar anime berdasarkan vektor fitur yang telah digabungkan sebelumnya. Perhitungan ditingkatkan dengan pembobotan fitur, karena tidak semua fitur memiliki pengaruh yang sama. Misalnya: genre lebih penting (lebih informatif) daripada durasi.

Langkah-langkah dalam fungsi:

- np.diag(weights): membuat matriks diagonal dari array bobot.
- features.dot(weights_matrix): menerapkan bobot pada masing-masing kolom fitur
- cosine_similarity(...): menghitung similarity antar baris (anime) berdasarkan sudut antar vektor fitur.

#### b. Menentukan Bobot untuk Setiap Fitur

Tidak semua fitur memiliki pengaruh yang sama terhadap persepsi kesamaan anime. Maka, diberi bobot agar model lebih peka terhadap fitur penting.

| Fitur                  | Bobot per fitur | Jumlah total bobot |
| ---------------------- | --------------- | ------------------ |
| Genre (20 dimensi SVD) | 0.4 per fitur   | 20 × 0.4 = 8.0     |
| Score                  | 0.3             | 0.3                |
| Duration               | 0.15            | 0.15               |
| Members                | 0.1             | 0.1                |
| Completion rate        | 0.05            | 0.05               |
| **Total**              | —               | **8.6**            |

### Model Rekomendasi

Fungsi hybrid_recommend() adalah inti dari sistem rekomendasi yang menggabungkan tiga pendekatan utama:

- Content-Based Filtering – berdasarkan anime yang mirip.
- Collaborative Filtering – berdasarkan rating anime oleh pengguna lain.
- Popular-Based (Fallback) – berdasarkan popularitas jika tidak ada input yang diberikan.

Selain itu, fungsi ini juga menyertakan:

Post-filtering berdasarkan kualitas anime: hanya anime dengan Skor ≥ 6.5 dan completion rate ≥ 30% yang ditampilkan.

✅ Mode 1 – Content-Based Filtering (jika anime_id diberikan)

    if anime_id:
    ...

Langkah-langkah:

- Cari index anime di anime_df berdasarkan MAL_ID.
- Ambil skor kemiripan terhadap semua anime lainnya.
- Urutkan skor dan pilih Top-N anime paling mirip (tanpa menyertakan dirinya sendiri).
- Lakukan post-filtering untuk menjaga kualitas rekomendasi.
- Kembalikan anime yang lolos filter.

🛑 Handling Error:

Jika anime_id tidak ditemukan di dataset:

Fungsi akan memberikan rekomendasi fallback berdasarkan popularitas.

outputnya:

=== CONTENT-BASED RECOMMENDATIONS ===

🔹 Anime: Cowboy Bebop (ID:20)

MAL_ID | Name | 	Genres | 	Score | 	completion_rate |
----- | ------------	| ---------------- | ----------------- | --------------- |
813 | 	Dragon Ball Z | 	Action Adventure Comedy Fantasy Martial Ar... | 	8.16 | 	0.871964 |
10686 | Naruto: Honoo no Chuunin Shiken! Naruto vs. Ko... | Action Adventure Martial Arts Shounen Supe... |	7.16 | 	0.884615 |
137 | 	Hunter x Hunter: Original Video Animation | 	Action Adventure Super Power Shounen | 	8.33 | 	0.839623 |
6033 | 	Dragon Ball Kai |  	Action Adventure Comedy Fantasy Martial Ar... | 	7.73 | 	0.702734 |
13667 | 	Naruto: Shippuuden Movie 6 - Road to Ninja | 	Action Adventure Super Power Martial Arts ... | 	7.67 | 	0.909860 |
594 | 	Naruto: Takigakure no Shitou - Ore ga Eiyuu Da... | Action Adventure Comedy Shounen Super Power | 	6.76 | 	0.926829 |
1735 | 	Naruto: Shippuuden | 	Action Adventure Comedy Super Power Martia... | 	8.16 | 	0.417952 |
10589 | 	Naruto: Shippuuden Movie 5 - Blood Prison | 	Action Adventure Martial Arts Super Power ... | 	7.46 | 	0.902294 |
10189 | 	Hunter x Hunter Pilot | 	Action Adventure Shounen Super Power | 	7.20 | 	0.752941 |
8246 | 	Naruto: Shippuuden Movie 4 - The Lost Tower | 	Action Comedy Martial Arts Shounen Super P... | 	7.42 | 	0.892743 |


👤 Mode 2 – Collaborative Filtering (jika user_id diberikan)

    elif user_id:
    ...
    
🔍 Penjelasan:

Fungsi memberikan rekomendasi berdasarkan anime yang disukai user (rating tertinggi oleh user tersebut). Langkah-langkah:

- Ambil seluruh rating dari user (user_id) di rating_df.
- Jika user belum pernah menilai anime (user baru), kembalikan rekomendasi populer.
- Pilih 3 anime dengan rating tertinggi dari user tersebut.
- Untuk setiap anime favorit tersebut, lakukan rekomendasi mirip menggunakan content-based filtering.
- Gabungkan hasil rekomendasi, hilangkan duplikat, dan filter kualitas dengan post-filter.

outputnya

=== COLLABORATIVE FILTERING ===

🔹 Recommendations for User ID: 1234

MAL_ID | Name | 	Genres | 	Score | 	completion_rate |
----- | ------------	| ---------------- | ----------------- | --------------- |
22265 | 	Free!: Eternal Summer | 	Slice of Life Comedy Sports Drama School | 	7.68 | 	0.742638 |
1764 | 	Slam Dunk (Movie) | 	Comedy Drama School Shounen Slice of Life ... | 	7.36 | 	0.778325 |
2499 | Slam Dunk: Hoero Basketman-damashii! Hanamichi... | Comedy Drama School Shounen Slice of Life ... | 	7.68 | 	0.744382 |
2498 | Slam Dunk: Shouhoku Saidai no Kiki! Moero Saku... | Comedy Drama School Shounen Slice of Life ... | 	7.58 | 	0.762178 |
1861 | 	Slam Dunk: Zenkoku Seiha Da! - Sakuragi Hanamichi | 	Slice of Life Comedy Sports Drama School ...|  	7.55|  	0.764045| 
14397 | 	Chihayafuru 2 | 	Drama Game Josei School Slice of Life Sports | 	8.43 | 	0.702797 |
36704 | 	Free!: Dive to the Future | 	Comedy Drama School Slice of Life Sports | 	7.59 | 	0.527100 |
30415 | 	High☆Speed!: Free! Starting Days | 	Comedy Drama School Slice of Life Sports | 	7.87  |	0.607401 |
20903 | 	Harmonie | 	Slice of Life Psychological Drama School | 	7.31 | 	0.703468 |
35507 | 	Youkoso Jitsuryoku Shijou Shugi no Kyoushitsu ... | 	Slice of Life Psychological Drama School | 	7.85 | 	0.740501 |

🌟 Mode 3 – Popular-Based Recommendation (Fallback)

    else:
    ...
    
🔍 Penjelasan:

Jika tidak diberikan anime_id maupun user_id, maka sistem akan menampilkan anime paling populer berdasarkan:

- Skor (Score) tertinggi
- Tingkat penyelesaian (completion_rate) tertinggi
- Filter dilakukan untuk menjaga kualitas hasil.


🧪 Post-Filtering

    def post_filter(df):
        return df[
            (df['Score'] >= score_threshold) &
            (df['completion_rate'] >= completion_threshold)
        ]
        
🔍 Penjelasan:

Filter ini bertujuan menyaring anime dengan kualitas rendah, agar hasil lebih relevan dan memuaskan. Nilai default filter adalah:

- Score ≥ 6.5
- completion_rate ≥ 0.3 (30%)

outputnya

=== Hybrid Filtering ===

🔹 Top 10 Overall Recommendations

MAL_ID | Name | 	Genres | Score | 	completion_rate |
----- | ------------	| ---------------- | ----------------- | --------------- |
5114 | 	Fullmetal Alchemist: Brotherhood | 	Action Military Adventure Comedy Drama Ma... | 	9.19 | 	0.732319 |
9253 | 	Steins;Gate | 	Thriller Sci-Fi | 	9.11 |  	0.696696 | 
38524 | 	Shingeki no Kyojin Season 3 Part 2 | 	Action Drama Fantasy Military Mystery Sho... | 	9.10 | 	0.873288 |
11061 | 	Hunter x Hunter (2011) | 	Action Adventure Fantasy Shounen Super Power | 	9.10 | 	0.647456 |
28977 | 	Gintama° | 	Action Comedy Historical Parody Samurai S... | 	9.10  |	0.478271 |
9969 | 	Gintama' | 	Action Sci-Fi Comedy Historical Parody Sa... | 	9.08 | 	0.561683 |
15417 | 	Gintama': Enchousen | 	Action Comedy Historical Parody Samurai S... | 	9.04 | 	0.677927 |
28851 | 	Koe no Katachi | 	Drama School Shounen | 	9.00 | 	0.818555 |
35180 | 	3-gatsu no Lion 2nd Season | 	Drama Game Seinen Slice of Life | 	9.00 | 	0.586541 |
34096 | 	Gintama. | 	Action Comedy Historical Parody Samurai S... | 	8.99 | 	0.624245 |


## 6. Evaluasi

Fungsi evaluate_models() bertujuan untuk menilai kinerja tiga model rekomendasi (Content-Based, Collaborative, dan Hybrid) berdasarkan precision, recall, dan F1-score dengan menggunakan metrik evaluasi standar dalam sistem rekomendasi. Fungsi ini mengukur akurasi sistem rekomendasi dalam mengenali anime yang disukai oleh pengguna, dan membandingkan hasil rekomendasi dengan ground truth. Alur Fungsi evaluate_models()

Input Parameter:

- user_sample: Sebuah sampel ID pengguna yang akan dievaluasi. Biasanya, ini adalah subset dari ID pengguna di dataset.
- top_n: Jumlah anime yang ingin direkomendasikan oleh sistem (default adalah 10).

Proses Evaluasi Model:

Fungsi ini bekerja dengan tiga model rekomendasi, yaitu Content-Based, Collaborative, dan Hybrid. Untuk setiap model:

- Ambil Ground Truth (anime yang disukai pengguna berdasarkan rating di atas threshold tertentu).
- Ambil Rekomendasi dari model.
  
Hitung Metrik Evaluasi:

- Precision: Persentase rekomendasi yang relevan di antara semua yang direkomendasikan.
- Recall: Persentase rekomendasi yang relevan di antara semua yang seharusnya direkomendasikan (ground truth).
- F1-Score: Harmonic mean dari Precision dan Recall.

Hasil Evaluasi:

Precision, recall, dan F1-score dihitung untuk masing-masing model. Hasil dihitung rata-rata untuk semua pengguna yang dievaluasi.

Output:

Sebuah DataFrame dengan hasil evaluasi untuk masing-masing model, yang meliputi:

- Model: Nama model (Content-Based, Collaborative, Hybrid).
- Precision: Rata-rata precision untuk model.
- Recall: Rata-rata recall untuk model.
- F1-Score: Rata-rata F1-score untuk model.
- User Evaluated: Jumlah pengguna yang dievaluasi.


### Hasil Evaluasi Model (Setelah Peningkatan):

| Model | Precision | Recall | F1-Score | EvaluatedScore |
| --- | --- | --- | --- | --- |
| Content-Based |	0.089 | 	0.51 | 	0.142 | 	100 |
| Collaborative | 0.108 | 	0.49 | 	0.167 | 	100 |
| Hybrid | 0.147 | 0.085 | 	0.44 | 	0.133 | 	100 |


### Interpretasi Hasil Evaluasi Model (Setelah Peningkatan)

Dari hasil evaluasi yang diberikan, kita dapat melihat bahwa semua model (Content-Based, Collaborative, dan Hybrid) menunjukkan nilai Precision, Recall, dan F1-Score yang serupa. Berikut adalah beberapa penjelasan untuk hasil tersebut:

- Precision: 0.084 - 0.106

   Precision mengukur seberapa banyak rekomendasi yang relevan di antara semua rekomendasi yang diberikan. Nilai precision yang relatif rendah ini menunjukkan bahwa banyak anime yang direkomendasikan oleh model tidak relevan dengan preferensi pengguna. Precision yang rendah ini bisa disebabkan oleh model yang memberikan rekomendasi berbasis similarity yang tidak sepenuhnya cocok dengan preferensi pengguna atau ketidakmampuan model dalam menangkap nuansa preferensi individual pengguna.

- Recall: 0.48 - 0.51

   Recall mengukur seberapa banyak anime yang relevan di antara semua yang seharusnya direkomendasikan. Nilai recall yang relatif tinggi ini menunjukkan bahwa model cukup baik dalam menemukan anime yang relevan untuk pengguna, namun masih ada ruang untuk perbaikan dalam mengidentifikasi semua anime yang relevan. Recall yang cukup baik ini menunjukkan bahwa model tidak terlalu banyak melewatkan anime yang disukai pengguna. Namun, beberapa anime yang seharusnya direkomendasikan mungkin masih hilang.

- F1-Score: 0.138 - 0.165

   F1-Score adalah rata-rata harmonis dari Precision dan Recall. Nilai F1-Score yang rendah ini menunjukkan bahwa meskipun recall cukup baik, precision-nya masih rendah, yang menarik perhatian pada trade-off antara precision dan recall. F1-Score yang rendah mengindikasikan bahwa meskipun model mampu menemukan beberapa anime relevan, kualitas rekomendasinya perlu lebih ditingkatkan.

- User Evaluated: 100

   Jumlah pengguna yang dievaluasi adalah 100, yang menunjukkan bahwa evaluasi mencakup sampel yang cukup besar, memberi gambaran yang lebih akurat mengenai kinerja model di seluruh pengguna.


## 7. User Input

Fungsi get_recommendation_input() dirancang untuk menerima input dari pengguna, memprosesnya, dan kemudian memberikan rekomendasi anime berdasarkan input tersebut. Fungsi ini menggabungkan interaksi dengan pengguna dan pemanggilan sistem rekomendasi berbasis hybrid. Langkah-langkah fungsi:

### a. Menampilkan Prompt Input:

Fungsi ini memulai dengan menampilkan dua prompt input bagi pengguna untuk memasukkan informasi:

- ID Anime: Menanyakan ID anime favorit pengguna (opsional).
- ID Pengguna: Menanyakan ID pengguna (opsional, misalnya, untuk menggunakan data pengguna yang sudah ada).

### b. Mengonversi Input:

Setelah menerima input dari pengguna, fungsi mencoba untuk mengonversi input yang dimasukkan ke dalam format yang benar:

- Jika input untuk anime_id dan user_id merupakan angka yang valid, mereka akan dikonversi ke dalam integer.
- Jika input tidak valid atau kosong, variabel anime_id dan user_id akan diatur ke None, yang artinya model akan menggunakan pendekatan fallback.
  
### c. Mencari Rekomendasi:

Fungsi memanggil hybrid_recommend() yang sebelumnya sudah dijelaskan, untuk mencari rekomendasi berdasarkan input yang diberikan. Fungsi ini mengambil anime_id, user_id, dan top_n (jumlah rekomendasi yang diinginkan). Fungsi akan mencoba menemukan rekomendasi berdasarkan metode hybrid yang menggabungkan content-based, collaborative, dan popular-based recommendations.


### d. Menampilkan Hasil Rekomendasi:

Setelah proses pencarian selesai, hasil rekomendasi ditampilkan menggunakan display(recommendations.reset_index(drop=True)). Ini menampilkan hasil dalam format yang lebih terstruktur (resetting index) dan mudah dibaca.


### e. Error Handling:

Jika terjadi kesalahan selama proses (misalnya, jika input tidak valid atau ada masalah dalam fungsi hybrid_recommend), fungsi menangani pengecualian tersebut dan menampilkan pesan error kepada pengguna.


| Input Diberikan        | Metode yang Digunakan              |
| ---------------------- | ---------------------------------- |
| `anime_id` saja        | Content-Based Filtering            |
| `user_id` saja         | Collaborative Filtering            |
| `anime_id` + `user_id` | Hybrid Filtering                   |
| Tidak ada              | Rekomendasi berdasarkan Popularity |

### Hasilnya

#### Jika user memasukan ID anime dan ID Pengguna maka model akan menampilkan hasil sebagai berikut
🎯 Sistem Rekomendasi Anime

Masukkan salah satu dari informasi berikut (atau keduanya):

Masukkan ID anime favorit Anda (kosongkan jika tidak ada): 1

Masukkan ID pengguna Anda (kosongkan jika tidak ada): 1

🔎 Mencari rekomendasi...

✨ Rekomendasi untuk Anda:

No | MAL_ID	| Name | Genres | Score |	completion_rate |
----- | ------------	| ---------------- | ----------------- | --------------- |	------------------- |
0 | 4037 | Cowboy Bebop: Yose Atsume Blues |	Action Adventure Comedy Drama Sci-Fi Space |	7.44 | 0.657283 |
1 |	1168 | Musekinin Kanchou Tylor OVA |	Adventure Comedy Drama Military Sci-Fi Space |	7.25 |	0.558442 |
2 |	2203 |	Waga Seishun no Arcadia: Mugen Kidou SSX |	Action Adventure Drama Sci-Fi Space |	7.40 |	0.429630 |
3 |	1651 |	Uchuu Senkan Yamato 2 |	Action Military Sci-Fi Adventure Space Drama |	7.42 |	0.461538 |
4 |	2202 |	Waga Seishun no Arcadia |	Action Adventure Drama Sci-Fi Space |	7.49 |	0.548523 |
5 |	1081 |	Space Pirate Captain Herlock: Outside Legend |	Action Adventure Space Drama Sci-Fi Seinen |	7.36 |	0.457143 |
6 |	2470 |	Uchuu Kaizoku Captain Herlock: Arcadia-gou no |	Action Sci-Fi Adventure Space Drama |	6.96 |	0.606061 |
7 |	3069 |	Yamato yo Towa ni |	Action Military Sci-Fi Adventure Space Drama |	6.61 |	0.460526 |
8 |	1645 |	Herlock Saga: Nibelung no Yubiwa |	Action Sci-Fi Adventure Space Drama Seinen |	6.71 |	0.571429 |
9 |	1336 |	Kyoushoku Soukou Guyver II |	Action Adventure Drama Horror Sci-Fi |	7.03 |	0.662100 |


#### Jika tidak memasukkan ID anime dan ID pengguna maka model akan menampilkan Top 10 Rekomendasi anime. berikut hasilnya

🎯 Sistem Rekomendasi Anime

Masukkan salah satu dari informasi berikut (atau keduanya):

Masukkan ID anime favorit Anda (kosongkan jika tidak ada): 

Masukkan ID pengguna Anda (kosongkan jika tidak ada): 

🔎 Mencari rekomendasi...

✨ Rekomendasi untuk Anda:
No | MAL_ID	| Name | Genres | Score |	completion_rate |
----- | ------------	| ---------------- | ----------------- | --------------- |	------------------- |
0 |	5114 |	Fullmetal Alchemist: Brotherhood	Action Military  | Adventure Comedy Drama Ma...	9.19 |	0.732319 |
1 |	9253 |	Steins;Gate	 | Thriller Sci-Fi |	9.11 |	0.696696 |
2 |	38524 |	Shingeki no Kyojin Season 3 Part 2 |	Action Drama Fantasy Military Mystery Sho... |	9.10 |	0.873288 |
3 |	11061 | Hunter x Hunter (2011) |	Action Adventure Fantasy Shounen Super Power |	9.10 |	0.647456 |
4 |	28977 |	Gintama° |	Action Comedy Historical Parody Samurai S... |	9.10 |	0.478271 |
5 |	9969 |	Gintama' |	Action Sci-Fi Comedy Historical Parody Sa... |	9.08 |	0.561683 |
6 |	15417 |	Gintama': Enchousen |	Action Comedy Historical Parody Samurai S... |	9.04 |	0.677927 |
7 |	28851 |	Koe no Katachi |	Drama School Shounen |	9.00 |	0.818555 |
8 |	35180 |	3-gatsu no Lion 2nd Season |	Drama Game Seinen Slice of Life |	9.00 |	0.586541 |
9 |	34096 |	Gintama. |	Action Comedy Historical Parody Samurai S... |	8.99 |	0.624245 |


## 8. Kesimpulan

Sistem rekomendasi anime yang dikembangkan berhasil menjawab permasalahan utama dalam pemilihan tontonan yang relevan dan menarik berdasarkan preferensi pengguna. Dengan mengombinasikan pendekatan Content-Based Filtering dan Collaborative Filtering dalam sebuah model hybrid, sistem ini mampu memberikan rekomendasi yang lebih akurat dan personal, sekaligus mengatasi tantangan klasik seperti cold start dan generalisasi rekomendasi.

Penerapan post-filtering berbasis skor dan completion rate juga berkontribusi signifikan dalam meningkatkan kualitas rekomendasi dengan hanya menampilkan anime dengan reputasi dan keterlibatan yang tinggi. Evaluasi model berdasarkan metrik Precision, Recall, dan F1-Score menunjukkan bahwa sistem telah mencapai performa yang memuaskan, khususnya dalam hal recall, yang penting dalam sistem rekomendasi karena memastikan bahwa sebagian besar anime relevan berhasil ditangkap oleh sistem.

Rekomendasi Pengembangan Selanjutnya

- Integrasi Data Mood/Emosi Pengguna

  Tambahkan analisis sentimen atau input mood pengguna untuk menyesuaikan rekomendasi dengan kondisi emosional, memperluas aspek personalisasi.

- Penerapan Deep Learning untuk Embedding Fitur

  Gunakan teknik seperti Neural Collaborative Filtering (NCF) atau Autoencoders untuk menangkap representasi laten dari preferensi pengguna dan fitur anime yang lebih kompleks.

- Peningkatan Collaborative Filtering Berbasis Matrix Factorization

  Terapkan Singular Value Decomposition (SVD) atau Alternating Least Squares (ALS) untuk mengoptimalkan prediksi rating dan hubungan antar pengguna.

- Penerapan Sistem Evaluasi Online (A/B Testing)

  Lakukan evaluasi nyata dengan pengguna sesungguhnya untuk mengukur dampak perubahan model terhadap keterlibatan pengguna secara langsung.

Daftar Referensi

Kaggle. (2020). Anime Recommendation Database 2020. https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database




