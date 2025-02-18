# Proyek Sistem Rekomendasi Buku 📚

Book-Recommendation-System

**Disusun oleh: Elisa Ramadanti**

---

## Project Overview 🌟

### Latar Belakang
Membuat sistem rekomendasi buku untuk membantu pengguna menemukan buku yang sesuai dengan preferensi mereka.

### Pentingnya Proyek
Buku adalah sumber pengetahuan yang sangat penting, tetapi jumlahnya yang besar sering kali membuat pengguna kesulitan memilih buku yang tepat.

### Riset/Referensi
- [Amazon](https://www.amazon.com/)
- [Google Books](https://books.google.com/)
- [Goodreads Recommendation System](https://www.goodreads.com/)

---

## Business Understanding 💼

### Problem Statements
1. Bagaimana membantu pengguna menemukan buku yang sesuai dengan preferensi mereka di antara ribuan pilihan yang tersedia?
2. Bagaimana memberikan rekomendasi yang relevan berdasarkan riwayat dan preferensi pengguna?

### Goals 🎯
1. Memberikan rekomendasi buku yang relevan dan sesuai dengan minat pengguna.
2. Meningkatkan pengalaman pengguna dalam mencari dan memilih buku.

### Solution Approach 🛠️
Untuk mencapai tujuan di atas, digunakan dua pendekatan sistem rekomendasi:
1. **Content-Based Filtering**: Merekomendasikan buku berdasarkan kesamaan konten, seperti deskripsi dan kategori buku.
2. **Collaborative Filtering**: Merekomendasikan buku berdasarkan interaksi pengguna, seperti rating yang diberikan pengguna terhadap buku.

---


## Data Understanding 📊
### Informasi Dataset

1. **Jumlah Data**: Dataset ini memiliki 6810 baris dan 12 kolom.

2. **Kondisi Data**
   
    - Terdapat beberapa missing values pada kolom subtitle, categories, thumbnail, description, published_year, average_rating, num_pages, dan ratings_count.
    - Tidak ada data duplikat berdasarkan pengecekan dengan `df.duplicated().sum()`.
      
3. **Sumber Data**: Dataset ini diambil dari Kaggle: [Books Dataset](https://www.kaggle.com/datasets/abdallahwagih/books-dataset)

   
5. **Uraian Fitur:**

   
| **Fitur**         | **Deskripsi**                                             |
|-------------------|-----------------------------------------------------------|
| **isbn13, isbn10** | Identifikasi unik buku menggunakan ISBN 13 atau ISBN 10. |
| **title, subtitle**| Informasi tentang judul buku dan subjudul (jika ada).    |
| **authors**        | Nama-nama penulis buku.                                  |
| **categories**     | Kategori atau genre buku.                                |
| **description**    | Deskripsi atau ringkasan isi buku.                       |
| **published_year** | Tahun publikasi buku.                                    |
| **average_rating** | Rating rata-rata buku berdasarkan ulasan pengguna.       |
| **num_pages**      | Jumlah halaman dalam buku.                               |
| **ratings_count**  | Jumlah total rating yang diterima oleh buku.             | 
|**ratings_count**   |Jumlah rating yang diterima                               |

6. **Tipe Data:**
    - Numerik: 4 kolom (published_year, average_rating, num_pages, ratings_count).
    - Objek/Teks: 7 kolom (isbn10, title, subtitle, authors, categories, thumbnail, description).
    - Integer: 1 kolom (isbn13).
---

## Data Preparation

**Tahapan Data Preparation:**
1. **Handling Missing Values:**
   Menghapus baris yang memiliki nilai null pada kolom yang akan digunakan untuk rekomendasi, seperti title, description, dan categories, untuk memastikan data yang bersih dan akurat.
2. **Text Preprocessing:**
  Mengubah teks dalam `description` menjadi huruf kecil dengan fungsi `preprocess_text()` untuk menghindari perbedaan akibat kapitalisasi huruf.

---

## Modeling and Result 💻

1. **Content-Based Filtering**:  Pendekatan ini memberikan rekomendasi berdasarkan kesamaan konten dari buku yang sudah ada, seperti deskripsi buku, kategori, atau penulis.
    -  **Cara Kerja**: Merekomendasikan buku berdasarkan kemiripan konten seperti deskripsi, kategori, dan penulis.  
    -  **Metode**: Menggunakan TF-IDF Vectorizer untuk mengubah teks menjadi representasi numerik, kemudian menghitung Cosine Similarity untuk mengukur kemiripan antar buku. Implementasi:
          - **TF-IDF Vectorizer** untuk mengubah teks deskripsi menjadi representasi numerik.
          - **Cosine Similarity** untuk mengukur kemiripan antar buku.

2.  **Collaborative Filtering**:  Pendekatan ini merekomendasikan buku berdasarkan pola interaksi pengguna lain yang serupa (misalnya, rating atau pembelian).
    - **Cara Kerja**: Merekomendasikan buku berdasarkan pola interaksi pengguna lain yang serupa (misalnya, rating).
    - **Metode:** Singular Value Decomposition (SVD) dari pustaka Surprise.

---

## Evaluation 📈

1. Content-Based Filtering 📝
Evaluasi untuk **Content-Based Filtering** dilakukan dengan menghitung **Cosine Similarity** antar buku untuk memberikan rekomendasi yang lebih akurat. Karena sistem ini berbasis pada konten buku itu sendiri, evaluasi Sistem ini menampilkan top-N rekomendasi.

Contoh penggunaan:

```python
content_based_recommendations("The Great Gatsby")
```

2. **Evaluasi Collaborative Filtering**: metrik yang digunakan adalah **RMSE (Root Mean Squared Error)**. Berikut adalah rumus untuk menghitung RMSE:

$$
RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (r_{ui} - \hat{r}_{ui})^2}
$$

Di mana:
- \( r_{ui} \) adalah rating asli yang diberikan oleh pengguna \( u \) untuk item \( i \),
- \( \hat{r}_{ui} \) adalah rating yang diprediksi oleh sistem,
- \( N \) adalah jumlah prediksi yang dihitung.

#### **Hasil Evaluasi**
- **RMSE (Root Mean Squared Error):**  
  - `0.3440`  
  - `0.34399586335267107`  
  Hasil ini menunjukkan akurasi model dalam memprediksi nilai dengan semakin kecilnya nilai RMSE, semakin baik performa model.

---

## Conclusion

* Content-Based Filtering berhasil memberikan rekomendasi buku yang relevan berdasarkan kemiripan deskripsi dan kategori buku, dengan menggunakan teknik TF-IDF dan Cosine Similarity.

* Collaborative Filtering efektif dalam memberikan rekomendasi berdasarkan pola interaksi pengguna lain, menggunakan pendekatan Singular Value Decomposition (SVD).

* Kedua metode menunjukkan bahwa sistem rekomendasi yang dibangun dapat memberikan hasil yang memadai untuk membantu pengguna memilih buku yang sesuai dengan preferensi mereka.

---


## 📌 Referensi
-  [Kaggle -Books Dataset](https://www.kaggle.com/datasets/abdallahwagih/books-dataset)
-  [Amazon](https://www.amazon.com/)
- [Google Books](https://books.google.com/)
- [Goodreads Recommendation System](https://www.goodreads.com/)

---


**Elisa Ramadanti**  
LinkedIn: [linkedin.com/in/elisa-ramadanti](https://www.linkedin.com/in/elisa-ramadanti)
