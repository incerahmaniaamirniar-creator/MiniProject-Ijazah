NAMA : INCE RAHMANIAR AMIR 
NIM : F1G124010
KELAS : A

**Alur Pemrosesan (Pipeline)**

Region of Interest (ROI) Cropping: Memotong area pada citra yang menjadi lokasi tanda tangan kepala sekolah sehingga proses analisis hanya dilakukan pada area yang diperlukan.

Grayscale Conversion: Mengubah citra ROI dari citra berwarna (RGB) menjadi citra grayscale untuk menyederhanakan proses pengolahan berdasarkan intensitas piksel.

Thresholding: Mengubah citra grayscale menjadi citra biner untuk memisahkan area tanda tangan (foreground) dari latar belakang (background). Metode yang digunakan meliputi Global Threshold, Otsu Threshold, dan Adaptive Threshold.

Morphological Operations:Opening digunakan untuk mengurangi noise atau piksel kecil yang tidak diperlukan.Closing digunakan untuk menutup celah dan menyambungkan bagian tanda tangan yang terputus.

Foreground Pixel Calculation: Menghitung jumlah atau persentase piksel foreground pada area ROI sebagai karakteristik untuk menentukan keberadaan tanda tangan.

Classification: Berdasarkan nilai foreground, citra diklasifikasikan menjadi:
SIGNATURE PRESENT → terdapat tanda tangan.
SIGNATURE ABSENT → tidak terdapat tanda tangan.

Evaluation: Hasil klasifikasi dibandingkan dengan kondisi sebenarnya menggunakan confusion matrix, accuracy, dan classification report.

**Hasil Pengujian** 

01_HighQuality_Enhanced.jpg.jpeg	7.18%	SIGNATURE PRESENT	SIGNATURE PRESENT

1	02_LowContrast.jpg.jpeg	7.29%	SIGNATURE PRESENT	SIGNATURE PRESENT

2	03_Blurred.jpg.jpeg	11.36%	SIGNATURE PRESENT	SIGNATURE PRESENT

3	04_HighNoise.jpg.jpeg	6.93%	SIGNATURE PRESENT	SIGNATURE PRESENT

4	05_LowResolution_Upsampled.jpg.jpeg	8.56%	SIGNATURE PRESENT	SIGNATURE PRESENT

5	06_Faded_Underexposed.jpg.jpeg	7.31%	SIGNATURE PRESENT	SIGNATURE PRESENT

6	07_ColorShift_WarmTint.jpg.jpeg	7.26%	SIGNATURE PRESENT	SIGNATURE PRESENT

7	08_JPEGCompression_Artifacts.jpg.jpeg	7.43%	SIGNATURE PRESENT	SIGNATURE PRESENT

8	09_CombinedDegradation.jpg.jpeg	8.20%	SIGNATURE PRESENT	SIGNATURE PRESENT

**Analisis dan Kesimpulan** 


1. Mengapa thresholding diperlukan sebelum analisis keberadaan tanda tangan?
   Thresholding diperlukan untuk memisahkan foreground dan background pada citra. Setelah citra diubah menjadi grayscale, thresholding mengubahnya menjadi citra biner sehingga area yang dianggap sebagai tanda tangan dapat dihitung berdasarkan jumlah atau persentase piksel foreground. Pada project ini digunakan Global Threshold, Otsu Threshold, dan Adaptive Threshold untuk membandingkan hasil segmentasi. 

3. Apa masalah jika threshold terlalu rendah atau terlalu tinggi?
   Jika threshold terlalu rendah: terlalu banyak piksel dapat dianggap sebagai foreground. Akibatnya noise atau bagian background dapat ikut terdeteksi sehingga nilai foreground menjadi terlalu besar.
   Jika threshold terlalu tinggi: sebagian piksel tanda tangan dapat dianggap sebagai background. Akibatnya detail tanda tangan dapat hilang atau terputus sehingga nilai foreground menjadi terlalu kecil.

3. Aturan klasifikasi
   Sistem menggunakan persentase foreground sebagai dasar klasifikasi. Pada notebook, batas klasifikasi yang digunakan adalah 5,0%. Jika persentase foreground ≥ 5,0%, hasil dikategorikan sebagai SIGNATURE PRESENT, sedangkan jika < 5,0%, dikategorikan sebagai SIGNATURE ABSENT. 

**Kesimpulan**

Mini project telah menerapkan ROI cropping, grayscale, Global Threshold, Otsu Threshold, Adaptive Threshold, morphological opening dan closing, perhitungan foreground pixel, serta klasifikasi SIGNATURE PRESENT/ABSENT. Hasil klasifikasi kemudian dievaluasi menggunakan confusion matrix, accuracy, dan classification report. 

