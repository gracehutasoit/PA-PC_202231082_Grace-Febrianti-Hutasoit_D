
# UAS Praktikum PCD D Grace

## Filtering Citra 
Filtering citra adalah teknik dalam pemrosesan citra yang digunakan untuk mengubah atau memperbaiki citra dengan menerapkan operasi matematika pada setiap piksel. Tujuannya bisa bervariasi, seperti mengurangi noise, menekankan fitur tertentu, atau memperbaiki kualitas citra.

Filter rata-rata adalah jenis filter linear yang menghitung rata-rata nilai piksel dalam sebuah jendela (kernel) yang meliputi piksel saat ini dan tetangganya.

Keuntungan: Filter rata-rata efektif dalam mengurangi noise acak, seperti noise Gaussian. Filter ini juga cukup sederhana dan cepat untuk dihitung.

Kelemahan: Filter ini juga dapat menyebabkan blur pada detail gambar dan tepi yang tajam, mengurangi ketajaman gambar.

# Penjelasan Kodingan 
### Pertama : 
import cv2 : untuk mengimpor pustaka OpenCV import matplotlib.pyplot as plt: mengimpor modul pyplot dari pustaka Matplotlib dengan alias plt. 
import numpy as np : mengimpor pustaka NumPy dengan alias np.

### Membaca gambar
img = cv2.imread("almet.jpg")
img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

### Ketetanggaan Piksel
copyImg1 = img.copy().astype(float) : Membuat salinan gambar img dan mengubah tipe datanya menjadi float

m1, n1 = copyImg1.shape : Menyimpan jumlah baris dan kolom gambar ke dalam variabel m1 dan n1 
output1 = np.empty([m1,n1]) : Membuat array kosong dengan ukuran yang sama seperti gambar asli.
#### Mencetak Ukuran dan Dimensi 
print("Shape copy citra 1 : ", copyImg1.shape)
print("Shape coutput citra 1 : ", output1.shape) : Mencetak ukuran gambar yang disalin dan array kosong

print('m1 : ', m1)
print('n1 : ', n1)
print() : Mencetak jumlah baris (m1) dan kolom (n1) gambar

### Membuat Filter Rata-Rata
for baris in range(0, m1-1): Iterasi melalui Baris yang berjalan dari 0 hingga m1-2
for kolom in range(0, n1-1) : Iterasi melalui kolom yang berjalan dari 0 hingga n1-2
a1 = baris : Menyimpan nilai baris saat ini ke dalam variabel a1
b1 = kolom : Menyimpan nilai kolom saat ini ke dalam variabel b1
jumlah = copyImg1[a1-1,b1-1] + copyImg1[a1-1,b1+1] +\
copyImg1[a1,b1-1] + copyImg1[a1,b1] + copyImg1[a1,b1+1] +\
copyImg1[a1+1,b1-1] + copyImg1[a1+1,b1] + copyImg1[a1+1,b1+1]
output1[a1, b1] = 1/9*jumlah : Menjumlahkan nilai dari 8 piksel tetangga dan piksel itu sendiri.

fig, axis = plt.subplots(1,2, figsize=(10,10)) : membuat sebuah figure Matplotlib dan dua subplot (1 baris, 2 kolom) menggunakan plt.subplots() dengan figsize=(10, 10).
ax = axis.ravel() : Mengubah array axis (yang berisi dua objek subplot) menjadi array 1D

ax[0].imshow(img, cmap='gray') : menampilkan gambar img pada subplot pertama (ax[0]) dengan skema warna grayscale (cmap='gray').
ax[0].set_title('Input Citra 1') : Memberi judul 'Input Citra 1' pada subplot pertama.

ax[1].imshow(output1, cmap='gray') : Menampilkan gambar output1 pada subplot kedua (ax[1]) dengan skema warna grayscale.
ax[1].set_title('Output Citra 1') : Memberi judul 'Output Citra 1' pada subplot kedua.
plt.show() : untuk menampilkan gambar.

### Membuat Filter Median
img = cv2.imread('almet.jpg') : Memuat gambar asli
img_median = img.copy() : untuk menyalin gambar dan disimpan dalam img_median.
img_median = cv2.cvtColor(img_median, cv2.COLOR_BGR2RGB) : untuk mengonversi citra dari skala abu-abu kembali ke RGB.

# Menerapkan filter median blur
img_median_after = cv2.medianBlur(img_median, 5) : untuk menerapkan filter median dengan ukuran kernel 5x5 pada img_median.

# Membuat subplot
fig, axis = plt.subplots(1, 2, figsize=(10, 10)) :  untuk membuat figur dengan 1 baris dan 2
kolom dengan ukuran 10x10.
ax = axis.ravel()

# Menampilkan gambar asli
ax[0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
ax[0].set_title('Gambar Asli') :  untuk membuat judul sublplot pertama menjadi Gambar Asli.

# Menampilkan gambar setelah difilter
ax[1].imshow(img_median_after)
ax[1].set_title('Gambar Filter Median') : untuk membuat judul sublplot kedua menjadi Gambar Filter Median.
plt.show() : untuk menampilka gambar.
