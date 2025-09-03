# Airbnb-Listings-Bangkok
Analisis data Airbnb di Bangkok untuk memahami distribusi harga berdasarkan lokasi (neighbourhood) dan jenis kamar (room type). Visualisasi dibuat menggunakan Python dan Tableau.
Repository ini berisi eksplorasi dan analisis data Airbnb di Bangkok. Tujuan utama dari analisis ini adalah untuk **Mengidentifikasi pola harga berdasarkan jenis kamar dan lokasi**.

--- 
🔑 Highlight dari analisis:

* 15.845 total penginapan terdata
* 50 area/neighbourhood yang tercover
* Median harga sekitar 1.429 THB/malam

---

📊 Tools yang digunakan:

* Python (pandas, matplotlib, seaborn) untuk data cleaning & eksplorasi
* Tableau untuk dashboard interaktif

---

📌 Insight ini dapat membantu wisatawan, host, maupun pelaku industri pariwisata dalam memahami pasar sewa jangka pendek di Bangkok.

--- 

## Dataset
Kita akan menganalisa data penginapan yang diperoleh dari dataset Airbnb Listings Bangkok. Dataset tersebut dapat diakses [di sini](https://drive.google.com/file/d/1pvU_zLJSXoPtsgUwGCnTNrMTRIdcpy1X/view?usp=sharing).
Ada beberapa kolom penting di dalam dataset Airbnb Listings Bangkok, yaitu:

* id : ID unik Airbnb untuk setiap penginapan (listing).
* name : Nama penginapan.
* host_id : ID unik Airbnb untuk pemilik/host.
* host_name : Nama host (biasanya nama depan).
* neighbourhood : Nama area/daerah tempat penginapan.
* latitude : Koordinat garis lintang penginapan.
* longitude : Koordinat garis bujur penginapan.
* room_type : Entire home/apt (seluruh unit), Private room (kamar pribadi), Shared room (bersama), atau Hotel.
* price : Harga sewa per malam (mata uang lokal).
* minimum_nights : Jumlah malam minimum yang harus dipesan.
* number_of_reviews : Jumlah ulasan yang diterima penginapan.
* last_review : Tanggal ulasan terakhir yang diberikan tamu.
* reviews_per_month : Rata-rata jumlah ulasan per bulan.
* calculated_host_listings_count : Jumlah listing lain yang dimiliki host di area tersebut.
* availability_365 : Jumlah hari penginapan tersedia dalam 1 tahun (0–365 hari).
* number_of_reviews_ltm : Jumlah ulasan yang diterima dalam 12 bulan terakhir.


**Note: Untuk definisi dalam bahasa inggris dapat dilihat [di sini](https://drive.google.com/file/d/1nUoZ-tQ3e3lmNzq-WMM4wNDV55-f_A5i/view?usp=sharing).**

---

## Data Cleaning

* Kolom `name` & `host_name` memiliki missing value yang value yang sangat kecil (< 0.1%). Oleh karena itu, baris yang kosong akan dihapus karena tidak memberikan informasi penting untuk analisa, dan penghapusan tidak akan mempengaruhi hasil analisis secara signifikan.
* Kolom `last_review` memiliki missing value sebesar 36.5%. Nilai kosong disini mengartikan bahwa penginapan tersebut **belum memiliki review**. Oleh karena itu, nilai NaN akan dibiarkan agar tetap bisa dianalisis perbedaan antara penginapan yang memiliki review vs tidak memiliki review.
* Kolom `review_per_month` memiliki missing value yang sinkron dengan `last_review`. Nilai kosong berarti tidak ada review sama sekali. untuk menjaga konsistensi perhitungan, nilai NaN akan diganti dengan angka '0'.

--- 

## Data Analysis

### Harga Penginapan Berdasarkan Jenis kamar
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/9bfb6e3c-f553-46a1-931f-b3476227d0da" />

<img width="859" height="547" alt="image" src="https://github.com/user-attachments/assets/40593f52-7cc1-407d-8045-0dc99e464511" />


Berdasarkan perhitungan **median (P50), P75, dan P90** harga sewa penginapan Airbnb di Bangkok menurut jenis kamar:

* **Entire home/apt**

  * Median harga berada di 1.536 THB per malam.

  * 90% listing memiliki harga ≤ 4.471 THB.

  * Ini menunjukkan sebagian besar unit apartemen/rumah utuh berada pada kisaran menengah hingga tinggi, sesuai ekspektasi karena penyewa mendapat akses penuh ke properti.

* **Hotel room**

  * Median harga sedikit lebih tinggi yaitu 1.700 THB, dan P90 mencapai 5.420 THB.

  * Hal ini menunjukkan bahwa harga hotel cenderung lebih bervariasi dan bisa lebih mahal dibanding apartemen, kemungkinan karena faktor layanan tambahan dan lokasi premium.

* **Private room**

  * Median harga 1.213 THB dengan P90 di 4.000 THB.

  * Kamar pribadi lebih murah dibanding entire home/apt atau hotel, namun tetap terdapat variasi harga hingga kelas menengah atas.

* **Shared room**

  * Jauh lebih murah, dengan median 500 THB dan P90 hanya 1.300 THB.

  * Hal ini memperlihatkan bahwa tipe shared room memang menyasar segmen budget-friendly.


### Harga Penginapan Berdasarkan Lokasi
<img width="702" height="701" alt="image" src="https://github.com/user-attachments/assets/0593dfe4-d402-4b77-8c5e-c64519657456" />

Scatter plot diatas menunjukkan distribusi harga Airbnb di Bangkok berdasarkan koordinat geografis (latitude & longitude) setelah dibatasi hingga persentil 90 (≤ P90) untuk mengurangi pengaruh outlier ekstrem.

Beberapa poin penting yang dapat disimpulkan:
* Mayoritas listing terkonsentrasi di area pusat kota Bangkok, terutama di sekitar koordinat **13.7 – 13.8 latitude** dan **100.5 – 100.6 longitude.**
* Warna biru muda mendominasi, menunjukkan bahwa sebagian besar penginapan berada pada kategori **harga menengah ke bawah** (sekitar < 2.000 THB per malam).
* Titik merah tersebar di area pusat, menandakan adanya beberapa listing dengan harga relatif lebih mahal, meski masih dalam batas ≤ P90.
* Area pinggiran kota cenderung memiliki listing dengan harga lebih rendah (lebih banyak titik biru muda).
* Sebaliknya, di kawasan pusat kota terdapat variasi harga lebih besar: dari penginapan murah hingga relatif mahal (gradasi warna dari biru hingga merah).
* Wisatawan dengan anggaran terbatas memiliki banyak pilihan di pinggiran maupun pusat kota.
* Listing dengan harga lebih tinggi terkonsentrasi di pusat kota, kemungkinan besar karena faktor lokasi strategis dekat pusat bisnis, transportasi umum, dan destinasi wisata utama.


### Harga Penginapan Berdasarkan Jenis kamar & Lokasi

<img width="1004" height="547" alt="image" src="https://github.com/user-attachments/assets/b8ae9d15-b63f-4dbe-8eae-df5621f65b20" />

Kesimpulan dari Heatmap diatas:
* Beberapa area pusat kota seperti **Phra Nakhon**, **Bang Rak**, **Vadhana**, dan **Khlong Toei** cenderung memiliki median harga lebih tinggi dibanding distrik lain.
* Hotel room umumnya memiliki median harga lebih tinggi dibanding Private room dan Shared room. Contoh ekstrem terlihat di **Chatu Chak**, di mana median harga Hotel room mencapai **4,944 THB**, jauh di atas tipe kamar lainnya di distrik yang sama
* Secara umum, Entire home/apt lebih mahal dibanding Private room, tetapi ada pengecualian di beberapa distrik seperti Phra Khanong, di mana harganya relatif sama (1,000 THB).
* Hampir di semua neighbourhood, Shared room punya median harga di bawah 600 THB. Ini menunjukkan segmen budget traveler masih cukup terlayani.

---

## Kesimpulan & Rekomendasi

### Kesimpulan

1. **Berdasarkan Jenis Kamar (Room Type)**
    * Entire home/apt dan Hotel room memiliki median harga lebih tinggi dibanding Private room dan Shared room.
    * Shared room konsisten menjadi opsi termurah di hampir semua kategori.

2. **Berdasarkan Lokasi (Neighbourhood)**
    * Distrik pusat kota seperti Phra Nakhon, Bang Rak, Vadhana, Ratchathewi, dan Khlong Toei cenderung lebih mahal.
    * Distrik pinggiran seperti Phra Khanong, Chatu Chak, dan Bang Khae relatif lebih murah.
    * Lokasi punya pengaruh besar terhadap harga, terutama karena akses ke pusat bisnis & destinasi wisata.

3. **Kombinasi Room Type + Neighbourhood**
    * Hotel room di Chatu Chak bisa sangat mahal (median 4,944 THB), sementara di area lain bisa jauh lebih murah.
    * Entire home/apt di Phra Nakhon dan Bang Rak berada di kelas harga menengah ke atas (>2,000 THB).
    * Shared room tetap menjadi pilihan termurah di semua distrik, dengan median di bawah 600 THB.

### Rekomendasi

1. **Untuk Host Airbnb**
    * Jika ingin **menargetkan segmen premium,** fokuslah membuka Entire home/apt atau Hotel room di area **Phra Nakhon**, **Bang Rak**, dan **Vadhana**, karena harga median di sana lebih tinggi dan pasarnya mendukung.
    * Jika ingin menarik **budget traveler**, Shared room atau Private room di area **Phra Khanong** atau **Chatu Chak** bisa jadi strategi yang tepat.

2. **Untuk Wisatawan**
    * Cari akomodasi dengan Private room di area **Ratchathewi** atau **Phra Khanong** untuk harga lebih terjangkau tapi tetap dekat dengan pusat kota.
    * Gunakan ***Shared room*** bila ingin opsi paling murah tanpa mengorbankan lokasi.

3. **Untuk Industri Pariwisata**
    * Pengembangan Infrastruktur & Aksesibilitas pada lokasi dengan harga relatif murah tapi jumlah listing banyak (contoh: Phra Khanong, Chatu Chak) bisa dipromosikan dengan peningkatan akses transportasi dan atraksi wisata.
    * Kolaborasi dengan Host Airbnb untuk membuat program promosi bersama, misal diskon akomodasi + tiket wisata
    * Harga di pusat kota sudah tinggi, dorong wisatawan untuk menjelajah area lain dengan kampanye “hidden gems of Bangkok”. Supaya dapat meningkatkan pemerataan ekonomi

---

*This app is created by Aditya Eka Putra. You can reach me through [GitHub](https://github.com/adityaeputra) or [Linkedin](https://www.linkedin.com/in/adityaeputra/).*
