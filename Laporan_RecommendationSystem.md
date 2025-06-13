# Laporan Proyek Machine Learning - Felix Taslim

## Project Overview

Menonton film merupakan salah satu kegiatan hiburan yang populer di kalangan masyarakat. Namun demikian, pengguna sering mengalami kesulitan dalam menentukan film apa yang ingin ditonton berikutnya, sehingga menghabiskan waktu lama hanya untuk memilih film yang sesuai dengan preferensi mereka. Permasalahan ini umum terjadi terutama karena banyaknya pilihan film yang tersedia di berbagai platform streaming.

Oleh karena itu, proyek ini bertujuan untuk mengembangkan sebuah **sistem rekomendasi film berbasis konten (Content-Based Filtering)** yang dapat memberikan saran film serupa berdasarkan film favorit pengguna. Dengan adanya sistem ini, diharapkan dapat membantu pengguna menemukan film-film yang relevan tanpa perlu melakukan pencarian manual secara berulang.

Menurut Ricci et al. (2011), sistem rekomendasi memiliki peranan penting dalam membantu pengguna menemukan informasi yang relevan dalam lingkungan di mana pilihan sangat berlimpah, seperti industri hiburan dan e-commerce [1].

## Business Understanding

### Problem Statements
- Bagaimana membantu pengguna menemukan film yang mirip atau relevan dengan film favorit mereka tanpa harus mencari secara manual?
- Bagaimana membangun sistem rekomendasi yang mampu merekomendasikan film berbasis kesamaan konten seperti genre, aktor, dan sutradara?

### Goals
- Membangun **sistem rekomendasi film Content-Based Filtering** yang dapat menyarankan film berdasarkan kesamaan fitur konten film terutama genre (genre, keywords, cast, director).
- Mengurangi waktu pencarian pengguna dalam menemukan film baru yang sesuai dengan preferensi film favorit mereka.

### Solution Approach
1. **Content-Based Filtering** (diimplementasikan):
   - Menggunakan informasi dari film itu sendiri seperti genre, kata kunci, pemain, dan sutradara.

## Data Understanding

Dataset yang digunakan merupakan dataset film dari Kaggle yang terdiri dari 24 variabel dan 4803 data film. Dataset ini memuat informasi seperti genre, keywords, sinopsis, sutradara, pemeran, tanggal rilis, popularitas, dll.

### Sumber Data:
[https://www.kaggle.com/datasets/abdallahwagih/movies](https://www.kaggle.com/datasets/abdallahwagih/movies)

### Variabel:
* `index`: Indeks baris (tidak relevan secara analitis, hanya penomoran)
* `budget`: Anggaran produksi film (dalam satuan USD)
* `genres`: Daftar genre film (misalnya: Action, Comedy)
* `homepage`: URL homepage resmi film
* `id`: ID unik film (biasanya dari TMDB)
* `keywords`: Kata kunci terkait film (tag-topik relevan)
* `original_language`: Bahasa asli film (misalnya: en, fr)
* `original_title`: Judul asli film dalam bahasa produksinya
* `overview`: Ringkasan atau deskripsi singkat alur cerita film
* `popularity`: Skor popularitas film (dihitung oleh TMDB berdasarkan beberapa faktor)
* `production_companies`: Daftar perusahaan produksi yang terlibat
* `production_countries`: Daftar negara tempat film diproduksi
* `release_date`: Tanggal rilis film
* `revenue`: Total pendapatan kotor film (dalam USD)
* `runtime`: Durasi film (dalam menit)
* `spoken_languages`: Bahasa-bahasa yang digunakan dalam film
* `status`: Status rilis film (misalnya: Released, Post Production)
* `tagline`: Slogan atau kalimat promosi film
* `title`: Judul film (dalam format publik)
* `vote_average`: Rata-rata skor penilaian dari pengguna TMDB
* `vote_count`: Jumlah total suara/penilaian yang diberikan pengguna
* `cast`: Daftar aktor/aktris utama yang membintangi film
* `crew`: Daftar tim kru produksi (editor, penulis, dll)
* `director`: Nama sutradara film

(Variabel lainnya seperti budget, revenue, runtime, homepage, dll tidak digunakan dalam model ini.)

### Exploratory Data Analysis (EDA):
- Melihat bentuk dataset dan tipe data pada dataset
  Terdiri dari 24 variabel dan 4803 data film. Tipe data berupa kategorikal dan numerikal.
- Melihat apakah ada missing value
  Ditemukan beberapa variabel yang memilki missing value dan akan ditangani di Data Preparation
- Melihat distribusi data pada dataset
  Dilakukan Univariate Data Analysis terhadap variabel kategorikal dan numerikal.

## Data Preparation

Tahapan data preparation meliputi:
1. **Seleksi fitur**: Dipilih fitur `genres`, `keywords`, `cast`, `director` untuk sistem rekomendasi.
2. **Handling missing values**: Missing values diisi string kosong ('') untuk teks agar dapat diproses TF-IDF.
3. **Fitur gabungan**: Semua fitur digabung menjadi satu string.
4. **Vectorization**: Digunakan TF-IDF Vectorizer dari Sklearn.

## Modeling and Result

Sistem rekomendasi menggunakan metode Content-Based Filtering berbasis TF-IDF dan Cosine Similarity. Cosine Similarity digunakan untuk mengukur kemiripan antar film.

Pada Modeling and Result berikut adalah tahapan yang dilakukan:
1. **Cosine Similarity**: Digunakan cosine_similarity dari Sklearn.
2. **Inference**

Contoh output rekomendasi (Top-10 Recommendation):

Masukkan judul film: Godfather

Rekomendasi film mirip dengan 'The Godfather':

1. The Godfather: Part III
2. The Godfather: Part II
3. Apocalypse Now
4. Closer
5. August Rush
6. West Side Story
7. Stomp the Yard
8. Leaving Las Vegas
9. American Graffiti
10. Love Actually

## Evaluation

Evaluasi dilakukan menggunakan metrik **Recommender System Precision**, yaitu persentase rekomendasi yang relevan dari Top-K hasil rekomendasi berdasarkan genre.

Contoh Evaluasi Recommender System Precision untuk "The Godfather":

| Judul Film             | Genre                       | Relevansi |
|-----------------------|----------------------------|-----------|
| The Godfather: Part III| Crime Drama Thriller        | Relevan   |
| The Godfather: Part II | Drama Crime                | Relevan   |
| Apocalypse Now        | Drama War                  | Relevan   |
| Closer                | Drama Romance              | Relevan   |
| August Rush           | Drama                      | Relevan   |
| West Side Story       | Crime Drama Music          | Relevan   |
| Stomp the Yard        | Drama Music                | Relevan   |
| Leaving Las Vegas     | Drama Romance              | Relevan   |
| American Graffiti     | Comedy Drama               | Relevan   |
| Love Actually         | Comedy Romance Drama       | Relevan   |

***Recommender System Precision: 100.00% (10/10 film relevan)**

Formula yang digunakan:

Recommender System Precision = (Jumlah item relevan) / (Jumlah item direkomendasikan)

Karena proyek ini tidak melibatkan data eksplisit interaksi pengguna, metrik seperti RMSE atau F1-score tidak digunakan.

Dengan hasil Recommender System Precision ini, kita bisa mengetahui bahwa sistem rekomendasi ini dapat digunakan untuk menyarankan film berdasarkan kesamaan fitur konten film dan tentunya akan mengurangi waktu pencarian pengguna dalam menemukan film baru yang sesuai dengan preferensi film favorit mereka.

## Referensi

[1] F. Ricci, L. Rokach, B. Shapira, and P.B. Kantor, “Recommender Systems Handbook”, Springer, 2011.
