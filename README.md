# Nama : Ahmad Raihan
# Project : Food Vision 101

## 1. Deskripsi Proyek
FoodVision101 App adalah Proyek berbasis deep learning yang membantu pengguna mengenali jenis makanan secara otomatis melalui analisis gambar. Selain fitur utama tersebut, tersedia juga fitur Artikel yang menyajikan informasi menarik mengenai 101 jenis makanan populer yang diklasifikasikan, seperti Burger, Pizza, Steak, Sushi, Pasta, Salad, Tacos, Donat, Es Krim, dan Nasi Goreng. Fitur ini bertujuan untuk memberikan edukasi tambahan bagi pengguna sebelum atau sesudah melakukan prediksi. Aplikasi ini menggunakan model deep learning yang telah diintegrasikan untuk klasifikasi gambar makanan secara akurat dan cepat.

## 2. Dataset
Adapun dataset yang digunakan dalam menyelesaikan proyek ini dapat dilihat pada tabel dibawah:
| Jenis | Keterangan |
| ------ | ------ |
| Title | Food 101 |
| Source | [Kaggle](https://www.kaggle.com/datasets/dansbecker/food-101) |
| Maintainer | [dansbecker⚡](https://www.kaggle.com/dansbecker) |
| License | Other (specified in description) |
| Visibility | Publik |
| Tags |Business |
| Usability | 6.88 |

## 3. Preview Gambar
- Adapun 12 kelas yang dipilih dalam pengerjaan project dapat dilihat gambarnya dibawah:
<img width="863" height="989" alt="Untitled" src="https://github.com/user-attachments/assets/1434925c-346d-4387-a678-33a8a8ad7e86" />

## 4. Model Evaluasi

### 4.1. Arsitektur Model

**1. 🎯 Mixed Precision Training**  
Model ini menggunakan teknik *mixed precision training* dengan kebijakan global `mixed_float16` untuk meningkatkan efisiensi memori dan kecepatan pelatihan model.

**2. 🧠 Pre-trained Model: EfficientNetB0**  
- Menggunakan arsitektur EfficientNetB0 yang telah dilatih pada ImageNet  
- `include_top=False` untuk menghapus layer klasifikasi asli  
- Semua layer dibekukan (`trainable=False`) untuk mempertahankan bobot pretrained  
- Ukuran input: **(224, 224, 3)**

**3. 🧪 Data Augmentasi (Sebagai Layer)**  
Teknik augmentasi gambar diterapkan langsung sebagai bagian dari arsitektur model:  
- *RandomFlip* (horizontal)  
- *RandomRotation* (15%)  
- *RandomZoom* (15%)  
- *RandomTranslation* (10%)

**4. 🏗️ Arsitektur Head Model**  
Struktur tambahan setelah feature extraction yang digunakan pada fine-tuning:  
- GlobalAveragePooling2D  
- Dense (256 unit, aktivasi ReLU)  
- Dropout (rate 0.5)  
- Dense (101 unit)  
- Aktivasi Softmax (`float32`) sebagai output

**5. ⚙️ Kompilasi Model**  
- Optimizer: Adam  
- Learning rate: 0.0001 (feature extraction) dan 0.00001 (fine-tuning)  
- Loss: SparseCategoricalCrossentropy  
- Metrik: Accuracy

**6. 📋 Ringkasan Arsitektur**  
Struktur model ditampilkan dengan `model.summary()` untuk melihat total parameter dan konfigurasi layer.
<img width="631" height="489" alt="image" src="https://github.com/user-attachments/assets/c073fb73-bdbf-4e45-b721-45e040ce23e5" />

### 4.2. Grafik Akurasi dan Loss 

<img width="567" height="455" alt="Untitled" src="https://github.com/user-attachments/assets/6d5a8bae-fa8a-4a37-a8e2-39fe43572f7b" />
<img width="567" height="455" alt="Untitled-1" src="https://github.com/user-attachments/assets/533ae8da-2e39-4625-a708-9542d8a96d4c" />

## 4.3 Performa Model berdasarkan Metrik Akurasi, Precision, Recall, dan Loss

