# Laporan Proyek Machine Learning - Melanie Sayyidina Sabrina Refman

## Project Overview

Sistem rekomendasi merupakan teknologi yang sangat penting di era digital untuk membantu pengguna menemukan item yang relevan dari jumlah pilihan yang sangat besar. Dalam proyek ini, sistem rekomendasi buku dibangun menggunakan Book Recommendation Dataset. Dataset ini mencakup informasi tentang buku, pengguna, dan penilaian buku, menjadikannya dataset yang cocok untuk membangun sistem rekomendasi berbasis konten.

Rekomendasi berbasis konten menggunakan fitur buku, seperti nama penulis, untuk menghitung kesamaan antar item. Model ini dirancang untuk membantu pengguna menemukan buku serupa berdasarkan preferensi mereka.

Referensi:

- F. Sun, Y. Shi and W. Wang, "Content-Based Recommendation System Based on Vague Sets," 2013 5th International Conference on Intelligent Human-Machine Systems and Cybernetics, Hangzhou, China, 2013, pp. 294-297, doi: 10.1109/IHMSC.2013.218.
- P. Mathew, B. Kuriakose and V. Hegde, "Book Recommendation System through content based and collaborative filtering method," 2016 International Conference on Data Mining and Advanced Computing (SAPIENCE), Ernakulam, India, 2016, pp. 47-52, doi: 10.1109/SAPIENCE.2016.7684166.

---

## Business Understanding

### Problem Statements

Pernyataan masalah yang diidentifikasi meliputi:

- Bagaimana sistem rekomendasi dapat membantu pengguna menemukan buku yang relevan?
- Bagaimana cara mengukur kesamaan antar buku berdasarkan atribut penulis?
- Bagaimana evaluasi performa model rekomendasi dilakukan untuk memastikan kualitas hasil?

### Goals

Tujuan proyek dirumuskan untuk menjawab pernyataan masalah, yaitu:

- Mengembangkan sistem rekomendasi berbasis konten yang memberikan rekomendasi buku berdasarkan kesamaan penulis.
- Menggunakan teknik TF-IDF dan cosine similarity untuk menghitung kesamaan antar buku.
- Mengevaluasi performa model menggunakan metrik precision, recall, dan F1-score.

### Solution Statements

- Teknik TF-IDF digunakan untuk merepresentasikan penulis buku dalam bentuk vektor numerik.
- Cosine similarity digunakan untuk mengukur kesamaan antar buku.

---

## Data Understanding

Dataset yang digunakan adalah [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). Dataset terdiri dari tiga file utama:

1. **Books.csv**: Berisi informasi tentang buku seperti ISBN, judul buku, penulis, tahun penerbitan, dan penerbit.
2. **Ratings.csv**: Berisi data penilaian pengguna terhadap buku (Book-Rating).
3. **Users.csv**: Berisi informasi pengguna, seperti lokasi dan usia.

### Informasi Dataset

#### Books

- Jumlah Data: 271.360 baris dan 8 kolom.

**Fitur Books**:

- ISBN: Identifikasi unik untuk buku.
- Book-Title: Judul buku.
- Book-Author: Penulis buku.
- Year-Of-Publication: Tahun penerbitan buku.
- Publisher: Nama penerbit buku.
- Image-URL-S: URL gambar sampul buku (ukuran kecil).
- Image-URL-M: URL gambar sampul buku (ukuran sedang).
- Image-URL-L: URL gambar sampul buku (ukuran besar).

**Kondisi Data**:

- Missing Value: Kolom "Book-Author" dan "Publisher" memiliki 2 nilai yang hilang, sedangkan kolom "Image-URL-L" memiliki 3 nilai yang hilang.
- Duplikat: Tidak ditemukan duplikasi.

#### Ratings

- Jumlah Data: 1.149.780 baris dan 3 kolom.

**Fitur Ratings**:

- User-ID: Identifikasi unik untuk pengguna.
- ISBN: Identifikasi unik untuk buku.
- Book-Rating: Penilaian buku oleh pengguna (0-10).

**Kondisi Data**:

- Missing Value: Tidak ditemukan nilai yang hilang.
- Duplikat: Tidak ditemukan duplikasi.
- Outlier: Penilaian berada dalam rentang 0-10, sehingga tidak ada outlier numerik.

#### Users

- Jumlah Data: 278.858 baris dan 3 kolom.

**Fitur Users**:

- User-ID: Identifikasi unik untuk pengguna.
- Location: Lokasi pengguna.
- Age: Usia pengguna.

**Kondisi Data**:

- Missing Value: Kolom "Age" memiliki banyak nilai yang hilang 110762.
- Duplikat: Tidak ditemukan duplikasi.

## Exploratory Data Analysis (EDA)

### Dataset Books

**Rincian Kolom**

- `ISBN`: Identifikasi unik untuk buku (**271,360 non-null**).
- `Book-Title`: Judul buku (**271,360 non-null**).
- `Book-Author`: Penulis buku (**271,358 non-null**).
- `Year-Of-Publication`: Tahun penerbitan buku (**271,360 non-null**).
- `Publisher`: Nama penerbit buku (**271,358 non-null**).
- `Image-URL-S`: URL gambar kecil buku (**271,360 non-null**).
- `Image-URL-M`: URL gambar medium buku (**271,360 non-null**).
- `Image-URL-L`: URL gambar besar buku (**271,357 non-null**).

**Tahun Publikasi**

- Terdapat data tahun publikasi yang tidak valid (seperti teks atau nilai kosong).
- Tahun publikasi diubah menjadi tipe numerik. Jika tidak valid, diisi dengan **0** untuk memastikan konsistensi tipe data.

**Pemilihan Kolom Relevan**

- Untuk analisis lebih lanjut, hanya kolom berikut yang digunakan:
  - `ISBN`
  - `Book-Title`
  - `Year-Of-Publication`
  - `Publisher`

**Penulis Paling Produktif**

- Grafik top 5 penulis dengan jumlah buku terbanyak disajikan.
- Informasi ini penting untuk memahami kontribusi penulis terhadap dataset.

### Dataset Ratings

**Rincian Kolom**

- `User-ID`: Identifikasi unik pengguna (**1,149,780 non-null**).
- `ISBN`: Identifikasi unik buku (**1,149,780 non-null**).
- `Book-Rating`: Penilaian buku (**1,149,780 non-null**).

**Distribusi Rating**

- Distribusi nilai penilaian pengguna ditampilkan melalui grafik.
- Hal ini membantu mengidentifikasi pola, seperti kecenderungan pengguna memberikan nilai tertentu.

### Dataset Users

**Rincian Kolom**

- `User-ID`: Identifikasi unik pengguna (**278,858 non-null**).
- `Location`: Lokasi pengguna (**278,858 non-null**).
- `Age`: Usia pengguna (**168,096 non-null**).

**Kondisi Data**

- Kolom `Age` memiliki **missing values** pada lebih dari 100,000 baris.
- Nilai usia tidak valid (contoh: nilai ekstrim atau kosong) diidentifikasi dan diisi/dikelola sesuai kebutuhan analisis.

---

## Data Preparation

### Menghapus Nilai yang Hilang

Pada tahap ini, dilakukan pemeriksaan dan penghapusan nilai yang hilang (`NaN`) hanya pada dataset `Books`. Kolom-kolom yang mengandung nilai hilang pada dataset `Books` dihapus untuk memastikan kualitas data yang digunakan dalam analisis. Sementara itu, dataset `Ratings` tidak mengandung nilai hilang, sehingga tidak diperlukan penghapusan. Pada dataset `Users`, meskipun ada nilai hilang, data tersebut tidak dihapus karena dianggap masih dapat digunakan dalam analisis.

### Menghapus Duplikasi

`ISBN` yang duplikat dapat menyebabkan ketidakkonsistenan dalam analisis. Oleh karena itu, entri dengan `ISBN` yang sama dihapus. Penghapusan duplikasi ini dilakukan pada dataset `Books` berdasarkan kolom `ISBN` untuk menjaga kualitas data. Hal ini penting agar tidak ada entri yang berulang, yang dapat mengganggu analisis atau mempengaruhi hasil model yang dibangun.

### Penggabungan Dataset

Dataset `Books` dan `Ratings` kemudian digabungkan berdasarkan kolom `ISBN`, menghasilkan satu dataset lengkap yang mencakup informasi tentang buku serta rating yang diberikan oleh pengguna. Penggabungan ini penting untuk mempersiapkan data yang akan digunakan dalam model rekomendasi, memungkinkan analisis yang lebih mendalam dan hubungan yang lebih baik antar data.

### Sampling Data

Karena ukuran dataset yang sangat besar, hanya 16.000 data pertama yang digunakan dalam analisis untuk mengurangi waktu pemrosesan. Dengan cara ini, proses pemodelan menjadi lebih cepat tanpa mengorbankan kualitas data yang signifikan. Dataset yang telah digabungkan dan disampling ini kemudian dimasukkan ke dalam variabel `ratings_books` untuk diproses lebih lanjut.

### Ekstraksi Fitur dengan TF-IDF

Untuk menganalisis data teks yang ada dalam kolom `Book-Author`, digunakan teknik **Term Frequency-Inverse Document Frequency** (TF-IDF) untuk mengubah teks menjadi representasi numerik yang dapat digunakan oleh model analisis lebih lanjut. Berikut adalah tahapan ekstraksi fitur menggunakan TF-IDF:

a. **Inisialisasi TF-IDF Vectorizer**

Pada tahap ini, `TfidfVectorizer` digunakan dengan parameter `stop_words='english'` untuk mengabaikan kata-kata yang tidak memberikan informasi berarti (stop words) dalam bahasa Inggris. Ini membantu agar model hanya berfokus pada kata-kata yang lebih relevan dalam kolom `Book-Author`.

b. **Perhitungan IDF**

Setelah inisialisasi, `TfidfVectorizer` digunakan untuk menghitung nilai Term Frequency (TF) dan Inverse Document Frequency (IDF) berdasarkan kolom `Book-Author`. Hasil dari perhitungan ini adalah matriks sparse yang berisi skor TF-IDF untuk setiap kata yang ada dalam teks `Book-Author`.

c. **Mendapatkan Nama Fitur**

Setelah perhitungan TF-IDF, nama fitur atau kata-kata unik yang muncul dalam teks diambil dengan menggunakan fungsi `get_feature_names_out()`. Kata-kata ini menjadi kolom dalam representasi numerik dari data teks.

d. **Mengubah Sparse Matrix ke DataFrame**

Matriks sparse yang berisi hasil perhitungan TF-IDF kemudian diubah menjadi DataFrame. Dalam DataFrame ini, indeksnya menggunakan `Book-Title`, dan kolom-kolomnya berisi kata-kata unik dari kolom `Book-Author`. Nilai dalam DataFrame adalah skor TF-IDF untuk setiap kata, yang memudahkan analisis lebih lanjut terhadap representasi numerik dari data teks.

---

## Modeling (Content-Based Filtering)

### Cosine Similarity

Pada pendekatan **Content-Based Filtering**, **Cosine Similarity** digunakan untuk mengukur tingkat kesamaan antara buku-buku berdasarkan vektor representasi yang diperoleh melalui **TF-IDF**. Cosine Similarity mengukur kesamaan antara dua vektor berdasarkan sudut antara keduanya. Nilai kesamaan ini berkisar antara -1 (berlawanan) hingga 1 (identik), dengan semakin kecilnya sudut, semakin mirip kedua vektor tersebut.

a. **Penghitungan Cosine Similarity**

Setelah fitur diekstraksi menggunakan **TF-IDF**, langkah berikutnya adalah menghitung **Cosine Similarity** antara pasangan buku. Proses ini menghasilkan skor kesamaan untuk setiap pasangan buku dalam dataset. Semakin tinggi skor kesamaan antara dua buku, semakin mirip keduanya dalam hal penulis, genre, atau tema yang dibahas.

b. **Matriks Cosine Similarity**

Hasil perhitungan **Cosine Similarity** adalah sebuah matriks yang menunjukkan seberapa mirip satu buku dengan buku lainnya. Matriks ini memiliki indeks yang merupakan judul buku, dan setiap nilai dalam matriks mencerminkan tingkat kesamaan antara dua buku yang berbeda. Matriks ini menjadi dasar untuk memberikan rekomendasi buku berdasarkan kesamaan yang ditemukan.

### Fungsi Rekomendasi Buku

Untuk memberikan rekomendasi buku yang relevan, sebuah fungsi `recommend_books` dibuat. Fungsi ini menerima judul buku sebagai input dan mengembalikan daftar 10 buku dengan kesamaan tertinggi. Jika judul buku yang diminta tidak ditemukan dalam dataset, fungsi ini akan memberikan pesan kesalahan yang sesuai.

#### Proses Rekomendasi:

1. **Input Judul Buku**: Pengguna memberikan judul buku yang ingin dijadikan acuan.
2. **Menghitung Kesamaan**: Sistem akan menghitung skor kesamaan antara buku yang dimasukkan dengan semua buku lainnya menggunakan **Cosine Similarity**.
3. **Penyajian Hasil**: Sistem mengembalikan 10 buku yang paling mirip dengan judul buku yang dimasukkan, berdasarkan skor kesamaan tertinggi.

Setelah implementasi sistem rekomendasi selesai, dilakukan pengujian menggunakan judul buku **"Into the Land of the Unicorns (Unicorn Chronicles)"**. Berikut adalah hasil rekomendasi buku yang paling mirip dengan buku tersebut:

### Top 10 Rekomendasi Buku

| No. | Rekomendasi Buku                                                                                |
| --- | ----------------------------------------------------------------------------------------------- |
| 1   | My Teacher Fried My Brains (MY TEACHER BOOKS)                                                   |
| 2   | Into the Land of the Unicorns (Unicorn Chronicles)                                              |
| 3   | A Glory of Unicorns                                                                             |
| 4   | Into the Land of the Unicorns (The Unicorn Chronicles, Book 1)                                  |
| 5   | Jeremy Thatcher, Dragon Hatcher                                                                 |
| 6   | My Teacher Fried My Brains (MY TEACHER BOOKS)                                                   |
| 7   | SPACE BRAT (SPACE BRAT 1)                                                                       |
| 8   | A Piece of My Mind: A Collection of Essays from the Journal of the American Medical Association |
| 9   | Das letzte Konzert.                                                                             |
| 10  | Sprinter (Hunter's Western Series)                                                              |

---

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

Hasil evaluasi menunjukkan bahwa model memiliki performa sempurna:

- Semua pasangan yang diprediksi sebagai similar benar-benar similar.
- Tidak ada kesalahan prediksi.

### Kesimpulan

Hasil evaluasi menunjukkan bahwa sistem rekomendasi berbasis konten berhasil memberikan rekomendasi buku yang relevan dengan tingkat akurasi yang sangat tinggi. Model ini dapat diterapkan untuk membantu pengguna menemukan buku berdasarkan preferensi mereka, khususnya berdasarkan atribut penulis. Dengan pengembangan lebih lanjut, model dapat diintegrasikan dengan atribut lain seperti genre atau sinopsis buku untuk memberikan rekomendasi yang lebih komprehensif.
