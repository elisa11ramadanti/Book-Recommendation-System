# Proyek Sistem Rekomendasi Buku 📚

Book-Recommendation-System

**Disusun oleh: Elisa Ramadanti**

---

## Project Overview 🌟

### Latar Belakang
Sistem rekomendasi buku menjadi semakin penting di era digital, di mana jumlah buku yang tersedia sangat besar dan pengguna sering kali kesulitan menemukan buku yang sesuai dengan preferensi mereka. Sistem ini bertujuan untuk membantu pengguna menemukan buku yang relevan berdasarkan riwayat interaksi mereka, seperti rating atau pembelian

### Pentingnya Proyek

Proyek ini penting karena:

1. Membantu pengguna menghemat waktu dalam mencari buku yang sesuai dengan minat mereka.
2. Meningkatkan pengalaman pengguna dalam menjelajahi konten baru.

### Riset/Referensi
- [Amazon](https://www.amazon.com/)
- [Google Books](https://books.google.com/)
- [Goodreads Recommendation System](https://www.goodreads.com/)

---

## Business Understanding 💼

### Problem Statements
*  Bagaimana memberikan rekomendasi yang relevan berdasarkan riwayat interaksi pengguna (seperti rating atau pembelian)?

### Goals 🎯
*  Mengembangkan sistem rekomendasi yang dapat memberikan rekomendasi buku yang akurat untuk meningkatkan kepuasan pengguna.

### Solution Approach 🛠️
*  Menggunakan Collaborative Filtering dengan merekomendasikan buku berdasarkan interaksi pengguna, seperti rating yang diberikan terhadap buku. Metode yang digunakan adalah Singular Value Decomposition (SVD) dari pustaka Surprise untuk memberikan rekomendasi berdasarkan pola interaksi pengguna lain yang memiliki preferensi serupa.

---

## Data Understanding 📊
### Informasi Dataset

1. **Jumlah Data**: Dataset ini memiliki 6810 baris dan 12 kolom.

2. **Kondisi Data**
   
    - Terdapat beberapa missing values pada kolom subtitle, categories, thumbnail, description, published_year, average_rating, num_pages, dan ratings_count.
    - Tidak ada data duplikat berdasarkan pengecekan dengan `df.duplicated().sum()`.
      
3. **Sumber Data**: Dataset ini diambil dari Kaggle: [Books Dataset](https://www.kaggle.com/datasets/abdallahwagih/books-dataset)

   
5. **Uraian Fitur Dataset :**

   
| **Fitur**         | **Deskripsi**                                             |
|-------------------|-----------------------------------------------------------|
| **isbn13, isbn10** | Identifikasi unik buku menggunakan ISBN 13 atau ISBN 10. |
| **title, subtitle**| Informasi tentang judul buku dan subjudul (jika ada).    |
| **authors**        | Nama-nama penulis buku.                                  |
| **categories**     | Kategori atau genre buku.                                |
| **thumbnail**      | URL gambar sampul buku.                                  |
| **description**    | Deskripsi atau ringkasan isi buku.                       |
| **published_year** | Tahun publikasi buku.                                    |
| **average_rating** | Rating rata-rata buku berdasarkan ulasan pengguna.       |
| **num_pages**      | Jumlah halaman dalam buku.                               |
| **ratings_count**  | Jumlah rating yang diterima oleh buku.                   | 


6. **Tipe Data:**
    - Numerik: 4 kolom (published_year, average_rating, num_pages, ratings_count).
    - Objek/Teks: 7 kolom (isbn10, title, subtitle, authors, categories, thumbnail, description).
    - Integer: 1 kolom (isbn13).
---

## Data Preparation

**Tahapan Data Preparation:**
1. **Menambahkan user_id Berdasarkan indeks:** Memberikan identifier unik untuk setiap user menggunakan indeks dataframe.
2. **Menangani missing values:** Menghapus missing values pada kolom average_rating dan ratings_count agar tidak memengaruhi perhitungan dalam sistem rekomendas
3. **Konversi Tipe Data**: Mengonversi tipe data isbn13 dan user_id menjadi string untuk memastikan konsistensi

* **Collaborative Filltering Preparation**
  1. **Persiapan Data untuk Surprise Library:** Menyiapkan data dengan kolom user_id, isbn13, dan average_rating untuk digunakan pada Surprise Library
  2. **Split Data:** Data dibagi menjadi dua bagian, train Set dan Test Set dengan proporsi 80%  dan 20% ini untuk mengevaluasi performa model rekomendasi secara efektif.
  
---

## Modeling and Result 💻

Pendekatan yang digunakan dalam proyek ini adalah Collaborative Filtering untuk menyelesaikan permasalahan rekomendasi buku dengan lebih efektif. 

### Collaborative Filtering:  

Pendekatan ini merekomendasikan buku berdasarkan pola interaksi pengguna lain yang serupa (misalnya, rating atau pembelian).

-  **Cara Kerja**:
   1. Collaborative Filtering bekerja dengan menganalisis kesamaan preferensi antar pengguna atau kesamaan karakteristik antar item.
   2. Dalam proyek ini, pendekatan ini merekomendasikan buku berdasarkan pola interaksi pengguna lain yang serupa, misalnya melalui rating yang diberikan pengguna terhadap buku-buku tertentu.
-  **Metode yang digunakan:**
     - Menggunakan Singular Value Decomposition (SVD) dari pustaka Surprise untuk mendekomposisi matriks interaksi pengguna-buku menjadi bentuk yang lebih sederhana.
     - Dengan SVD, pola kesamaan pengguna atau item dapat ditemukan lebih mudah, sehingga rekomendasi yang dihasilkan lebih akurat dan relevan.
       
### **Top-N Recommendation**
- Digunakan untuk menampilkan N buku teratas dengan prediksi rating tertinggi bagi pengguna tertentu.

Hasil rekomendasi ditampilkan dalam bentuk tabel peringkat yang memuat informasi berikut: 

- Rank: Urutan rekomendasi berdasarkan prediksi rating tertinggi.
- Judul Buku: Judul buku yang direkomendasikan.
- Prediksi Rating: Nilai prediksi rating dari model SVD.
  
Berikut adalah contoh **Top-5 rekomendasi buku** menggunakan **Collaborative Filtering** dengan metode **SVD** untuk User 3:  

| **Rank** | **Judul Buku**                  | **Prediksi Rating** |
|----------|---------------------------------|---------------------|
| 1        | Justine                         | 4.28                |
| 2        | Babar the King                  | 4.28                |
| 3        | Children of the Mind            | 4.27                |
| 4        | Night of the Long Shadows       | 4.27                |
| 5        | The Kate DiCamillo Collection   | 4.27                |  

Berikut Hasil Visualisasi **Top-5 rekomendasi buku** menggunakan **Collaborative Filtering** dengan metode **SVD** untuk User 3:

 ![Top-5 rekomendasi buku user 3](https://github.com/user-attachments/assets/7add86fc-1ab5-4e68-aeda-a43a86d327c0)


---

## Evaluation 📈

### **Metrik evaluasi yang digunakan**:  
1. RMSE (Root Mean Squared Error):
   
   Mengukur rata-rata kesalahan kuadrat antara nilai prediksi dan nilai aktual. Semakin kecil nilai RMSE, semakin akurat model dalam memprediksi rating. Berikut adalah rumus untuk menghitung RMSE:

$$
RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (r_{ui} - \hat{r}_{ui})^2}
$$

Di mana:
- \( r_{ui} \) adalah rating asli yang diberikan oleh pengguna \( u \) untuk item \( i \),
- \( \hat{r}_{ui} \) adalah rating yang diprediksi oleh sistem,
- \( N \) adalah jumlah prediksi yang dihitung.
   
2. MAE (Mean Absolute Error):
  
   Mengukur rata-rata kesalahan absolut antara nilai prediksi dan nilai aktual. MAE lebih fokus pada besar kecilnya kesalahan secara absolut tanpa mempertimbangkan arah kesalahan. Berikut adalah rumus untuk menghitung MAE:

$$
MAE = \frac{1}{N} \sum_{i=1}^{N} \left| r_{ui} - \hat{r}_{ui} \right|
$$  

Di mana:  
- \( r_{ui} \) adalah rating asli yang diberikan oleh pengguna \( u \) untuk item \( i \),  
- \( \hat{r}_{ui} \) adalah rating yang diprediksi oleh sistem,  
- \( N \) adalah jumlah prediksi yang dihitung.


#### **Hasil Evaluasi Model menggunakan Test Set**

| Metrik   | Nilai  |
|----------|--------|
| **RMSE** | 0.2473 |
| **MAE**  | 0.1736 |


#### **Hasil Evaluasi Model menggunakan Test Set**

| Metrik   | Fold 1 | Fold 2 | Fold 3 | Fold 4 | Fold 5 | Mean   | Std    |
|----------|--------|--------|--------|--------|--------|--------|--------|
| **RMSE** | 0.3168 | 0.3391 | 0.3756 | 0.3195 | 0.3009 | 0.3304 | 0.0257 |
| **MAE**  | 0.2175 | 0.2365 | 0.2368 | 0.2333 | 0.2318 | 0.2312 | 0.0071 |  


---


## Conclusion
- Sistem rekomendasi buku berhasil dibangun menggunakan Collaborative Filtering dengan metode SVD.
- Model memberikan rekomendasi yang relevan berdasarkan pola interaksi pengguna lain yang memiliki preferensi serupa.
- Hasil evaluasi menunjukkan RMSE sebesar 0.2473 dan MAE sebesar 0.1736, menandakan prediksi yang akurat.
- Top-5 rekomendasi buku berhasil ditampilkan dengan prediksi rating tertinggi bagi pengguna.
- Sistem ini membantu pengguna menemukan buku yang sesuai dengan preferensi mereka, meningkatkan pengalaman membaca.

---


## 📌 Referensi
- [Kaggle -Books Dataset](https://www.kaggle.com/datasets/abdallahwagih/books-dataset)
- [Amazon](https://www.amazon.com/)
- [Google Books](https://books.google.com/)
- [Goodreads Recommendation System](https://www.goodreads.com/)

---

**Elisa Ramadanti**  
LinkedIn: [linkedin.com/in/elisa-ramadanti](https://www.linkedin.com/in/elisa-ramadanti)
