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
- Membangun **sistem rekomendasi film Content-Based Filtering** yang dapat menyarankan film berdasarkan kesamaan fitur konten film (genre, keywords, cast, sutradara).
- Mengurangi waktu pencarian pengguna dalam menemukan film baru yang sesuai dengan preferensi film favorit mereka.

### Solution Approach
1. **Content-Based Filtering** (diimplementasikan):
   - Menggunakan informasi dari film itu sendiri seperti genre, kata kunci, pemain, dan sutradara.
2. **Collaborative Filtering** (opsional — tidak diimplementasikan):
   - Menggunakan data interaksi pengguna lain (seperti rating atau penilaian film), yang belum diterapkan dalam proyek ini karena keterbatasan data eksplisit dari pengguna.

## Data Understanding

Dataset yang digunakan merupakan dataset film dari TMDB yang terdiri dari 24 variabel dan 4803 data film. Dataset ini memuat informasi seperti genre, kata kunci, sinopsis, sutradara, pemeran, tanggal rilis, popularitas, dll.

### Sumber Data:
https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata

### Variabel:
- genres: Daftar genre film.
- keywords: Kata kunci terkait film.
- tagline: Slogan film.
- title: Judul film.
- cast: Daftar aktor utama.
- director: Sutradara film.

(Variabel lainnya seperti budget, revenue, runtime, homepage, dll tidak digunakan dalam model ini.)

### Exploratory Data Analysis (EDA):
- Data kategori seperti 'genres', 'cast', 'keywords' diperiksa distribusinya.
- Data numerik (vote count, vote average) divisualisasikan distribusinya.
- Tidak ada missing value kritikal pada fitur yang dipilih.

## Data Preparation

Tahapan data preparation meliputi:
1. **Seleksi fitur**: Dipilih fitur `genres`, `keywords`, `tagline`, `title`, `cast`, `director` untuk sistem rekomendasi.
2. **Handling missing values**: Missing values diisi string kosong ('') untuk teks agar dapat diproses TF-IDF.
3. **Fitur gabungan**: Semua fitur digabung menjadi satu string.
4. **Vectorization**: Digunakan TF-IDF Vectorizer.

## Modeling and Result

Sistem rekomendasi menggunakan metode Content-Based Filtering berbasis TF-IDF dan Cosine Similarity. Cosine Similarity digunakan untuk mengukur kemiripan antar film.

Contoh output rekomendasi (Top-10 Recommendation):

Masukkan judul film: The Godfather

Rekomendasi film mirip dengan 'The Godfather':

1. The Godfather: Part II
2. The Godfather: Part III
3. Scarface
4. Goodfellas
5. Casino
6. A Bronx Tale
7. Donnie Brasco
8. Carlito's Way
9. American Gangster
10. Heat

## Evaluation

Evaluasi dilakukan menggunakan **Precision@K**, yaitu persentase rekomendasi yang relevan dari Top-K hasil rekomendasi berdasarkan genre.

Contoh Evaluasi Precision@10 untuk "The Dark Knight":

| Judul Film            | Genre                           | Relevansi     |
|---------------------|----------------------------------|--------------|
| Batman Begins        | Action Adventure Crime           | Relevan      |
| Man of Steel         | Action Adventure Sci-Fi          | Relevan      |
| ...                 | ...                              | ...          |

**Precision@10: 100.00% (10/10 film relevan)**

Formula yang digunakan:

Precision@K = (Jumlah item relevan) / (Jumlah item direkomendasikan)

Karena proyek ini tidak melibatkan data eksplisit interaksi pengguna, metrik seperti RMSE atau F1-score tidak digunakan.

## Referensi

[1] F. Ricci, L. Rokach, B. Shapira, and P.B. Kantor, “Recommender Systems Handbook”, Springer, 2011.
