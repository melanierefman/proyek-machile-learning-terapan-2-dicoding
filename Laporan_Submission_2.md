# Laporan Proyek Machine Learning - Melanie Sayyidina Sabrina Refman

## Project Overview

Sistem rekomendasi adalah teknologi yang sangat penting di era digital untuk membantu pengguna menemukan item yang relevan dari jumlah pilihan yang sangat besar. Dalam proyek ini, kami membangun sistem rekomendasi buku menggunakan Book Recommendation Dataset. Dataset ini mencakup informasi tentang buku, pengguna, dan penilaian buku, menjadikannya dataset yang cocok untuk membangun sistem rekomendasi berbasis konten.

Rekomendasi berbasis konten menggunakan fitur buku, seperti nama penulis, untuk menghitung kesamaan antar item. Model ini membantu pengguna menemukan buku serupa berdasarkan preferensi mereka.

Referensi:

- F. Sun, Y. Shi and W. Wang, "Content-Based Recommendation System Based on Vague Sets," 2013 5th International Conference on Intelligent Human-Machine Systems and Cybernetics, Hangzhou, China, 2013, pp. 294-297, doi: 10.1109/IHMSC.2013.218.
- P. Mathew, B. Kuriakose and V. Hegde, "Book Recommendation System through content based and collaborative filtering method," 2016 International Conference on Data Mining and Advanced Computing (SAPIENCE), Ernakulam, India, 2016, pp. 47-52, doi: 10.1109/SAPIENCE.2016.7684166.

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:

- Bagaimana sistem rekomendasi dapat membantu pengguna menemukan buku yang relevan?
- Bagaimana cara mengukur kesamaan antar buku berdasarkan atribut penulis?
- Bagaimana evaluasi performa model rekomendasi dilakukan untuk memastikan kualitas hasil?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:

- Mengembangkan sistem rekomendasi berbasis konten yang memberikan rekomendasi buku berdasarkan kesamaan penulis.
- Menggunakan teknik TF-IDF dan cosine similarity untuk menghitung kesamaan antar buku.
- Mengevaluasi performa model menggunakan metrik precision, recall, dan F1-score.

### Solution Statements

- Menggunakan algoritma TF-IDF untuk merepresentasikan penulis buku dalam bentuk vektor numerik.
- Menggunakan cosine similarity untuk mengukur kesamaan antar buku.

## Data Understanding

Dataset yang digunakan adalah [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). Dataset terdiri dari tiga file utama:

1. **Books.csv**: Berisi informasi tentang buku seperti ISBN, judul buku, penulis, tahun penerbitan, dan penerbit.
2. **Ratings.csv**: Berisi data penilaian pengguna terhadap buku (Book-Rating).
3. **Users.csv**: Berisi informasi pengguna, seperti lokasi dan usia.

### Informasi Dataset:

#### Books:

- ISBN: Identifikasi unik untuk buku.
- Book-Title: Judul buku.
- Book-Author: Penulis buku.
- Year-Of-Publication: Tahun penerbitan buku.
- Publisher: Nama penerbit buku.

#### Ratings:

- User-ID: Identifikasi unik untuk pengguna.
- ISBN: Identifikasi unik untuk buku.
- Book-Rating: Penilaian buku oleh pengguna (0-10).

#### Users:

- User-ID: Identifikasi unik untuk pengguna.
- Location: Lokasi pengguna.
- Age: Usia pengguna.

### Exploratory Data Analysis (EDA)

- **Distribusi Rating Buku**: Mayoritas penilaian adalah nol, menunjukkan data implisit.
- **Top 5 Penulis dengan Buku Terbanyak**: Penulis paling produktif diidentifikasi untuk analisis lebih lanjut.

## Data Preparation

### Tahapan Data Preparation:

1. **Mengubah Tipe Data**: Tahun penerbitan pada dataset Books diubah menjadi integer dengan mengganti nilai yang tidak valid menjadi 0.
2. **Menghapus Nilai yang Hilang**: Kolom dengan nilai hilang pada dataset Books, Ratings, dan Users diperiksa dan dihapus.
3. **Menghapus Duplikasi**: ISBN yang duplikat pada dataset Books dihapus.
4. **Penggabungan Dataset**: Dataset Books dan Ratings digabungkan berdasarkan ISBN untuk mendapatkan dataset yang lengkap.
5. **Sampling Data**: Karena ukuran dataset besar, hanya 16.000 data pertama yang digunakan untuk mengurangi waktu pemrosesan.

## Modeling

### Model Content-Based Filtering

- **TF-IDF Vectorizer**: TF-IDF digunakan untuk merepresentasikan teks (penulis buku) dalam bentuk vektor numerik.
- **Cosine Similarity**: Digunakan untuk mengukur kesamaan antar buku berdasarkan vektor TF-IDF.
- **Fungsi Rekomendasi**: Fungsi recommend_books mengambil judul buku sebagai input dan memberikan 10 rekomendasi buku berdasarkan kesamaan kosinus.

## Evaluation

### Metrik Evaluasi

Model dievaluasi menggunakan metrik:

1. **Precision**: Proporsi prediksi positif yang benar.
2. **Recall**: Proporsi item relevan yang ditemukan.
3. **F1-Score**: Rata-rata harmonis antara precision dan recall.

### Hasil Evaluasi

- **Precision**: 1.00
- **Recall**: 1.00
- **F1-Score**: 1.00

Model memiliki performa sempurna, menunjukkan bahwa:

- Semua pasangan yang diprediksi sebagai similar benar-benar similar.
- Tidak ada kesalahan prediksi.

### Kesimpulan

Hasil evaluasi menunjukkan bahwa sistem rekomendasi berbasis konten berhasil memberikan rekomendasi buku yang relevan dengan tingkat akurasi yang sangat tinggi. Model ini dapat diterapkan untuk membantu pengguna menemukan buku berdasarkan preferensi mereka, khususnya berdasarkan atribut penulis. Dengan pengembangan lebih lanjut, model dapat diintegrasikan dengan atribut lain seperti genre atau sinopsis buku untuk memberikan rekomendasi yang lebih komprehensif.
