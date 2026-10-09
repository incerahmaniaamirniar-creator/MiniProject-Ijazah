**1**. **Penjelasan Metode & Hasil Evaluasi Mini Project Verifikasi Ijazah1.** 
Penjelasan Metode yang DigunakanDalam prototype ini, digunakan serangkaian pemrosesan citra digital (image processing pipeline) untuk membaca nomor ijazah dan mengidentifikasi keberadaan tanda tangan secara otomatis:Grayscale Conversion: Mengubah citra masukan berwarna (BGR) menjadi 1 saluran (single-channel) warna abu-abu. Tahap ini bertujuan untuk mempercepat komputasi dan menghilangkan distorsi variasi warna kertas atau warm tint.   Image Enhancement (CLAHE): Mengaplikasikan Contrast Limited Adaptive Histogram Equalization. CLAHE membagi citra menjadi ubin-ubin kecil (tiles) dan meratakan kontras secara lokal tanpa memicu over-enhancement pada area latar belakang kertas.   Region of Interest (ROI) Cropping: Memotong area spesifik berdasarkan koordinat proporsional citra. Area bawah-kiri difokuskan untuk pembacaan nomor ijazah, sedangkan area kanan-bawah difokuskan untuk area tanda tangan.   Binarization (Otsu's Thresholding): Mengubah citra abu-abu pada ROI menjadi citra biner hitam-putih secara adaptif. Nilai ambang (threshold) ditentukan otomatis untuk memisahkan piksel teks/tinta dari latar belakang.   Optical Character Recognition (OCR): Menggunakan mesin Tesseract OCR pada ROI nomor ijazah biner untuk mengonversi piksel teks angka menjadi string teks digital.Morphological Processing (Closing): Mengaplikasikan operasi dilasi yang diikuti erosi menggunakan kernel bujursangkar (3x3) pada ROI tanda tangan. Teknik ini menyambungkan piksel goresan tinta yang terputus agar membentuk objek tanda tangan yang utuh.   Signature Detection: Menghitung rasio piksel tinta (non-zero pixels) pada ROI tanda tangan. Jika rasio piksel tinta melebihi ambang batas minimum (> 0.01), sistem mengategorikan tanda tangan sebagai PRESENT, dan jika kurang maka ABSENT. 

**2**. **Analisis Efektivitas Metode Enhancement Berdasarkan Nilai CERPengujian nilai Character Error Rate (CER) dilakukan dengan membandingkan teks hasil OCR terhadap Ground Truth nomor ijazah (571012022000056) pada 9 variasi kondisi citra. **  
Analisis Hasil Pengujian:CLAHE (Paling Efektif): CLAHE menghasilkan tingkat akurasi tertinggi dengan nilai CER 0.0% pada hampir seluruh kondisi citra (termasuk Low Contrast, Faded, Color Shift, dan JPEG Compression). Pengecualian terjadi pada kondisi High Noise ekstrem di mana pembacaan OCR terganggu. CLAHE sangat efektif karena menyesuaikan kontras secara lokal sehingga karakter angka tetap tajam.   Grayscale Saja: Mampu mencapai CER 0.0% pada sampel beresolusi standar, namun tidak adaptif apabila diuji pada citra dengan pencahayaan yang sangat tidak merata atau pudar.   Histogram Equalization Global (Sangat Tidak Efektif): Menghasilkan nilai CER sangat buruk (> 80.0%) pada seluruh sampel. Metode global ini menaikkan kontras secara agresif pada seluruh area gambar, sehingga noise latar belakang kertas ikut membesar dan membingungkan mesin OCR.   Kesimpulan: Metode enhancement yang paling efektif adalah CLAHE, karena terbukti menjaga akurasi OCR (nilai CER terendah) secara stabil di berbagai variasi degradasi citra.

**3**. ##  **How to Run Code (Panduan Menjalankan Program)**

### 1. Persiapan Environment
1. Buka [Google Colab](https://colab.research.google.com/).
2. Buat notebook baru (`.ipynb`) atau unggah file notebook yang ada di repository ini.
3. Siapkan ke-9 file gambar sampel ijazah (`01_HighQuality_Enhanced.jpg.jpeg` hingga `09_CombinedDegradation.jpg.jpeg`) di folder lokal komputer kamu.

### 2. Tahapan Eksekusi Sel Kode

#### **Langkah 1: Instalasi Library & Engine Tesseract OCR**
Di sel pertama, program akan memasang paket `tesseract-ocr` ke dalam sistem operasi Linux Colab. Selain itu, sel ini juga menginstal pustaka-pustaka Python yang dibutuhkan seperti `pytesseract` (untuk interface OCR), `opencv-python` (untuk pengolahan citra), `matplotlib` (untuk visualisasi), `pandas` (untuk membuat tabel), dan `python-Levenshtein` (untuk menghitung nilai CER).

#### **Langkah 2: Unggah & Konversi Awal ke Grayscale**
Jalankan sel kedua untuk mengunggah ke-9 file gambar ijazah secara bersamaan menggunakan fitur `files.upload()`. Setelah proses unggah selesai, sistem secara otomatis membaca tiap file, mengubah warnanya dari BGR menjadi *Grayscale* (1 channel warna), dan menampilkan hasil visual 9 citra abu-abu tersebut dalam bentuk *grid 3x3*.

#### **Langkah 3: Preprocessing Image Enhancement (CLAHE)**
Sel ketiga memproses ke-9 citra *grayscale* menggunakan metode **CLAHE** (*Contrast Limited Adaptive Histogram Equalization*). Metode ini membagi citra menjadi ubin-ubin kecil untuk menaikkan kontras secara adaptif dan lokal. Hasil pemrosesan ditampilkan kembali agar kita bisa melihat perbedaan tingkat ketajaman kontras teks sebelum dan sesudah diaplikasikan CLAHE.

#### **Langkah 4: Pemotongan Region of Interest (ROI Cropping)**
Pada sel keempat, sistem melakukan pemotongan area spesifik berdasarkan koordinat proporsional dari ukuran citra:
- **Area Nomor Ijazah**: Dipotong pada bagian kiri bawah citra.
- **Area Tanda Tangan**: Dipotong pada bagian kanan bawah citra.
Sel ini akan menampilkan gambar pasangan potongan ROI (Nomor & Tanda Tangan) untuk masing-masing dari ke-9 ijazah.

#### **Langkah 5: Binarisasi, Morfologi, dan Ekstraksi Output Teks**
Sel kelima merupakan tahap pemrosesan utama dan ekstraksi informasi:
1. **Area Nomor**: Diberikan binarisasi *Otsu Thresholding* menjadi hitam-putih, lalu dibaca oleh Tesseract OCR untuk mengekstrak string angka nomor ijazah.
   
2. **Area Tanda Tangan**: Diberikan binarisasi terbalik (*Otsu Thresholding Inv*) dan dilanjutkan dengan operasi morfologi *Closing* (kernel 3x3) untuk menyambungkan garis tinta. Rasio piksel tinta dihitung; jika melebihi ambang batas (`> 0.01`), maka tanda tangan dideteksi sebagai `PRESENT`.
   
3. **Display Output**: Tampilan biner/morfologi diposisikan bersandingan dan format teks dicetak langsung sesuai standar permintaan dosen:
   ```text
   Input:
   01_HighQuality_Enhanced.jpg.jpeg

   Output:
   Nomor Ijazah : 571012022000056
   Tanda Tangan : PRESENT

**Langkah 6: Evaluasi Nilai CER (Character Error Rate)**
Di sel terakhir, program melakukan pengujian perbandingan akurasi pembacaan OCR terhadap Ground Truth (571012022000056). Sistem akan menguji 3 variasi teknik enhancement (Grayscale Saja, CLAHE, dan Histogram Equalization Global) pada ke-9 file ijazah, lalu menghitung jarak Levenshtein-nya untuk menampilkan Tabel Evaluasi Nilai CER secara otomatis di layar.
