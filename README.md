# Analisis Perbandingan Arsitektur Vision Transformer untuk Klasifikasi Citra Makanan Indonesia

Repositori ini berisi kode implementasi untuk penelitian komparatif mengenai kinerja tiga arsitektur Vision Transformer: ViT (Vision Transformer), DeiT (Data-efficient Image Transformer), dan Swin Transformer pada dataset Indonesian Food.

## Deskripsi Proyek

Penelitian ini bertujuan untuk mengevaluasi performa ketiga model tersebut dalam mengklasifikasikan 13 jenis makanan tradisional Indonesia. Eksperimen dilakukan dengan strategi Full Fine-Tuning menggunakan framework PyTorch dan library Hugging Face Transformers.

## Struktur File

Proyek ini terdiri dari tiga notebook terpisah untuk memastikan isolasi lingkungan eksekusi dan manajemen memori GPU yang optimal:

1.  `ViT.ipynb`: Kode pelatihan dan evaluasi untuk model ViT Base.
2.  `DeiT.ipynb`: Kode pelatihan dan evaluasi untuk model DeiT Base (Distilled).
3.  `Swin.ipynb`: Kode pelatihan dan evaluasi untuk model Swin Transformer Base.

## Prasyarat Lingkungan

Kode ini dirancang untuk dijalankan di lingkungan Google Colab dengan spesifikasi berikut:

* **Platform:** Google Colab
* **Hardware Accelerator:** GPU (Disarankan T4 atau lebih tinggi)
* **Bahasa Pemrograman:** Python 3.10+
* **Library Utama:**
    * PyTorch & Torchvision
    * Transformers (Hugging Face)
    * Scikit-learn
    * Pandas & Matplotlib

## Dataset

Dataset yang digunakan adalah **Indonesian Food Dataset** yang bersumber dari Kaggle.

* **Sumber:** Kaggle - [Indonesian Food Dataset](https://www.kaggle.com/datasets/rizkyyk/dataset-food-classification) (rizkyyk)
* **Total Citra:** 6.500 gambar
* **Jumlah Kelas:** 13 Kelas (Ayam Goreng, Bakso, Rendang, Sate, dll.)
* **Distribusi:** 500 gambar per kelas

## Cara Menjalankan Kode

Disarankan untuk menjalankan notebook satu per satu hingga selesai untuk menghindari error "Out of Memory" (OOM) pada sesi Colab.

### Langkah 1: Persiapan Token Kaggle
Siapkan file `kaggle.json` (API Token dari akun Kaggle Anda) untuk mengunduh dataset secara otomatis di dalam notebook.

### Langkah 2: Eksekusi Notebook
Lakukan langkah berikut untuk setiap file `.ipynb` (ViT, DeiT, dan Swin):

1.  Buka file notebook di Google Colab.
2.  Pastikan Runtime menggunakan GPU:
    * Menu: **Runtime** > **Change runtime type** > Pilih **T4 GPU**.
3.  Jalankan sel pertama. Anda akan diminta untuk mengunggah file `kaggle.json`.
4.  Anda akan diminta untuk melakukan Mount Google Drive. Izinkan akses ini untuk keperluan penyimpanan model terbaik (*checkpoint*).
5.  Jalankan seluruh sel secara berurutan (*Run All*).

### Langkah 3: Penyimpanan Model
Setelah pelatihan selesai, model dengan akurasi validasi terbaik akan otomatis disimpan di Google Drive Anda pada path berikut:
* `/content/drive/My Drive/ViT_Project/`

## Konfigurasi Eksperimen

Seluruh model dilatih menggunakan konfigurasi hiperparameter yang seragam untuk memastikan perbandingan yang adil (*fair comparison*):

| Parameter | Nilai / Metode |
| :--- | :--- |
| **Resolusi Input** | 224 x 224 pixel |
| **Batch Size** | 32 |
| **Epochs** | 5 |
| **Learning Rate** | 5e-5 |
| **Optimizer** | AdamW |
| **Loss Function** | Cross Entropy Loss |
| **Augmentasi Data** | RandomResizedCrop, HorizontalFlip, Rotation, ColorJitter |

## Output dan Metrik Evaluasi

Setiap notebook akan menghasilkan laporan evaluasi pada Test Set yang mencakup:

1.  **Spesifikasi Model:** Jumlah total parameter, parameter yang dapat dilatih, dan ukuran file model (MB).
2.  **Metrik Klasifikasi:** Akurasi (Accuracy), Presisi (Precision), Recall, dan F1-Score.
3.  **Visualisasi:**
    * Kurva Pembelajaran (Loss dan Akurasi terhadap Epoch).
    * Confusion Matrix (Matriks Kesalahan Prediksi).
4.  **Performa Waktu Nyata:** Rata-rata waktu inferensi per citra (milidetik) dan throughput (gambar/detik).

## Catatan Penting

* **Konflik Ukuran Input:** Kode untuk DeiT dan Swin telah dimodifikasi secara manual (hardcoded size = 224) untuk mengatasi perbedaan konfigurasi default pada library Transformers, memastikan input citra sesuai dengan tensor yang diharapkan model.
* **Kapasitas Penyimpanan:** Pastikan Google Drive memiliki ruang kosong yang cukup (minimal 2 GB) untuk menyimpan ketiga file model hasil pelatihan.
* **Link File Bobot Model: [Link Gdrive](https://drive.google.com/drive/folders/1TtLf31BJwmYn16gC-GJfcGd0EtnN4hMW?usp=sharing)**
