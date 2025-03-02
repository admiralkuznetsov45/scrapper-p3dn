# Dokumentasi Scrapping Data TKDN Kemenperin

## Tujuan

Dokumen ini menjelaskan proses *scraping* data dari situs web Kementerian Perindustrian, khususnya data sertifikat Tingkat Komponen Dalam Negeri (TKDN). Data yang diperoleh akan disimpan dalam format JSON untuk analisis lebih lanjut.

# Tools dan Library yang Digunakan dalam Scrapping Data TKDN

## 1. Python

* Bahasa pemrograman utama untuk menulis skrip *scraping*.

## 2. Selenium

* Pustaka untuk mengotomatiskan browser web (Chrome).
* Digunakan untuk navigasi halaman, interaksi dengan elemen web, dan ekstraksi data dari halaman web dinamis.

## 3. WebDriver (Chrome)

* Driver untuk mengontrol browser Chrome melalui Selenium.
* Menghubungkan Selenium dengan browser Chrome.

## 4. `asyncio` dan `nest_asyncio`

* `asyncio`: Pustaka standar Python untuk operasi asinkron.
* `nest_asyncio`: Untuk menjalankan loop peristiwa asinkron di lingkungan yang tidak mendukung loop peristiwa bertingkat.
* Digunakan untuk menjalankan beberapa tugas secara bersamaan, meningkatkan efisiensi.

## 5. `os`

* Pustaka untuk berinteraksi dengan sistem operasi.
* Digunakan untuk membuat folder penyimpanan data.

## 6. `json`

* Pustaka untuk bekerja dengan data dalam format JSON.
* Digunakan untuk menyimpan data hasil *scraping* dalam format JSON.

## 7. `datetime`

* Pustaka untuk manajemen tanggal dan waktu.
* Digunakan untuk membuat nama file yang unik dengan menambahkan timestamp.

## 8. `time`

* Pustaka untuk menambahkan penundaan dalam eksekusi skrip.
* Digunakan untuk menghindari pembebanan server web dan memastikan halaman web memuat sepenuhnya.

## 9. `selenium.webdriver.support.ui.WebDriverWait` dan `selenium.webdriver.support.expected_conditions as EC`

* Digunakan untuk menunggu elemen web tertentu muncul atau kondisi terpenuhi sebelum melanjutkan eksekusi skrip.

## Sumber Data

Data diperoleh dari situs web:

-   Halaman utama: [https://tkdn.kemenperin.go.id/rekap.php](https://tkdn.kemenperin.go.id/rekap.php)
-   Halaman detail kelompok barang (dengan parameter `kd`): [https://tkdn.kemenperin.go.id/sertifikat_idx.php?kd=1](https://tkdn.kemenperin.go.id/sertifikat_idx.php?kd=1), [https://tkdn.kemenperin.go.id/sertifikat_idx.php?kd=2](https://tkdn.kemenperin.go.id/sertifikat_idx.php?kd=2), dst.


## Kelompok Barang

Data dikelompokkan berdasarkan kategori barang dengan kode `kd` sebagai berikut:
1: "Bahan Penunjang Pertanian"
2: "Mesin dan Peralatan Pertanian"
3: "Mesin dan Peralatan Pertambangan"
4: "Mesin dan Peralatan Migas"
5: "Alat Berat, Konstruksi dan Material Handling"
6: "Mesin dan Peralatan Pabrik"
7: "Bahan Bangunan/Konstruksi"
8: "Logam dan Barang Logam"
9: "Bahan Kimia dan Barang Kimia"
10: "Peralatan Elektronika"
11: "Peralatan Kelistrikan"
12: "Peralatan Telekomunikasi"
13: "Alat Transport"
14: "Bahan dan Peralatan Kesehatan"
15: "Peralatan Laboratorium"
16: "Komputer dan Peralatan Kantor"
17: "Pakaian dan Perlengkapan Kerja"
18: "Peralatan Olahraga dan Pendidikan"
19: "Sarana Pertahanan"
20: "Barang Lainnya"

## Proses Scrapping

1.  **Input Kode Kelompok Barang (kd):** Pengguna diminta memasukkan kode kelompok barang (1-20) yang ingin di-*scraping*.
2.  **Input Batas Halaman (Opsional):** Pengguna dapat memasukkan jumlah halaman yang ingin di-*scraping*. Jika dibiarkan kosong, semua halaman akan di-*scraping*.
3.  **Buka URL Kelompok Barang:** Skrip akan membuka URL yang sesuai dengan kode `kd` yang diinput.
4.  **Ekstraksi Data:** Skrip akan mengekstrak data dari tabel yang ada di halaman web, termasuk:
    -   Perusahaan
    -   Jenis Produk
    -   Spesifikasi
    -   Tipe
    -   Merk
    -   Nilai TKDN
5.  **Navigasi Halaman (Pagination):** Jika ada lebih dari satu halaman, skrip akan menavigasi ke halaman berikutnya dan mengulangi proses ekstraksi data.
6.  **Penyimpanan Data:** Data yang diekstrak akan disimpan dalam format JSON dengan struktur sebagai berikut: