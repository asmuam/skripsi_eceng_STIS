# Deteksi dan Pemetaan Tumbuhan Asing Invasif Eceng Gondok dengan Citra Satelit dan Machine Learning (Studi Kasus: Danau Rawa Pening, Kabupaten Semarang)

Repositori ini berisi keseluruhan proyek skripsi, mencakup kode pemodelan, dataset publik, serta kode sumber untuk aplikasi web visualisasi di Google Earth Engine (GEE).

---

### **Informasi Peneliti**

| Keterangan           | Informasi                                                                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **NIM**              | `222111840`                                                                                                                                             |
| **Nama**             | Adib Sulthon Muammal                                                                                                                                    |
| **Judul Skripsi**    | Deteksi dan Pemetaan Tumbuhan Asing Invasif Eceng Gondok dengan Citra Satelit dan Machine Learning (Studi Kasus: Danau Rawa Pening, Kabupaten Semarang) |
| **Dosen Pembimbing** | Dr. Drs. Waris Marsno, M.Stat.                                                                                                                          |

---

### **Deskripsi Singkat**

Penelitian ini berfokus pada pengembangan sistem untuk mendeteksi dan memetakan sebaran eceng gondok (_Eichhornia crassipes_) di Danau Rawa Pening. Proses deteksi memanfaatkan data citra satelit yang diolah dengan menggunakan algoritma _machine learning_.

Hasil akhir dari penelitian ini adalah sebuah **aplikasi web (_web app_) visualisasi** 🗺️ yang dibangun menggunakan Google Earth Engine. Aplikasi ini menampilkan peta sebaran eceng gondok secara interaktif, di mana aset hasil pengolahan data diimpor langsung ke dalam platform GEE untuk divisualisasikan.

---

### **Aplikasi Web Visualisasi (Artefak Utama)**

Artefak utama dari penelitian ini adalah aplikasi web interaktif yang dapat diakses melalui tautan berikut:

- **Tautan Utama:** [**https://222111840.users.earthengine.app/view/deteksi-eceng-gondok-rawa-pening-2024**](https://222111840.users.earthengine.app/view/deteksi-eceng-gondok-rawa-pening-2024)
- **Tautan Pendek:** [**https://s.stis.ac.id/AppVizEceng**](https://s.stis.ac.id/AppVizEceng)

Kode sumber untuk membangun aplikasi web ini terdapat pada file `web`.

---

### **Struktur Folder Proyek**

```
.
├── aset/
│   └── (Berisi data-data yang diperlukan untuk mereplikasi proyek
│          dan data-data hasil eksekusi proyek)
├── agustus.js
├── juni.js
├── juli.js
├── web.js
├── skripsi_eceng.ipynb
├── LICENSE
└── README.md
```

---

### **Panduan Penggunaan dan Alur Kerja Detail**

Proyek ini memiliki alur kerja yang terbagi antara Google Earth Engine (untuk akuisisi data dan visualisasi) dan lingkungan Python (untuk pemodelan).

#### **Alur Kerja Proyek**

1.  **Tahap 1: Akuisisi & Ekstraksi Data (Google Earth Engine)**

    - Skrip GEE (`juni`, `juli`, `agustus`) digunakan untuk mengumpulkan citra satelit Sentinel-1 & Sentinel-2.
    - Proses ini mencakup _cloud masking_, perhitungan berbagai indeks, dan penggabungan band.
    - Data sampel kemudian diekstraksi berdasarkan titik-titik label (Eceng, KJA, Air, dll.) yang didefinisikan sebagai _Geometry_ atau _FeatureCollection_ di GEE.
    - Hasil akhirnya adalah data tabular (misalnya `.csv`) yang **diekspor** dari GEE untuk digunakan pada tahap pemodelan.

2.  **Tahap 2: Pemodelan & Klasifikasi (Lokal - Python)**

    - Data tabular yang diekspor dari GEE menjadi input untuk notebook `skripsi_eceng.ipynb`.
    - Di dalam notebook ini, model _Machine Learning_ (Random Forest) dan _Deep Learning_ (CNN) dilatih dan diuji.
    - Output dari tahap ini adalah **citra klasifikasi dalam format GeoTIFF (`.tif`)** untuk setiap bulan dan setiap model.

3.  **Tahap 3: Visualisasi & Aplikasi Web (Google Earth Engine)**
    - File `.tif` hasil klasifikasi dari tahap 2 **diimpor kembali** ke Google Earth Engine sebagai _Image Asset_.
    - Skrip `web` kemudian menggunakan aset-aset citra klasifikasi ini untuk membangun antarmuka pengguna (UI) aplikasi web, lengkap dengan legenda, pemilih layer, dan panel inspeksi data.

#### **Langkah-langkah Replikasi**

Untuk mereplikasi proyek ini dari awal, ikuti langkah-langkah berikut:

**1. Persiapan Awal di Google Earth Engine (GEE)**

- **Login ke GEE:** Buka [Google Earth Engine Code Editor](https://code.earthengine.google.com/).
- **Unggah Aset Batas Wilayah:** Unggah data batas wilayah studi (misalnya, `rawa_pening_shp`, `rawa_pening_sbwp`, dan `roi`) sebagai aset ke akun GEE Anda.
- **Siapkan Titik Label:** Titik-titik label untuk klasifikasi (Eceng Gondok, Air, dll.) dibuat sebagai _FeatureCollection_ langsung di GEE. Jika Anda mereplikasi, Anda perlu membuat titik-titik label Anda sendiri di area studi atau untuk hasil replikasi gunakan variabel import label pada masing-masing kode GEE yang tersedia.
- **Jalankan Skrip Akuisisi Data:**
  1.  Buat skrip baru di GEE untuk setiap file di (`juni`, `juli`, `agustus`).
  2.  Salin-tempel kode dari file-file tersebut ke dalam skrip GEE yang sesuai.
  3.  **PENTING:** Ubah path aset di bagian `import` dan `export` pada skrip agar menunjuk ke aset batas wilayah dan folder Google Drive Anda.
  4.  Jalankan setiap skrip. Tujuan utamanya adalah untuk **mengekspor data tabular** (misalnya, ke Google Drive) yang akan digunakan untuk pemodelan.

**2. Proses Pemodelan di Google Colab**

- **Siapkan Google Drive:**
  1.  Buat folder proyek (misal, `Skripsi_Eceng`) di Google Drive.
  2.  Unggah data `.csv` dari GEE ke folder `data`.
  3.  Unggah notebook `skripsi_eceng.ipynb` ke folder utama proyek.
- **Buka dan Jalankan Notebook di Colab:**
  1.  Buka notebook `skripsi_eceng.ipynb` dari Google Drive Anda menggunakan Google Colab.
  2.  Jalankan **sel pertama (Set-Up)** untuk menginstal semua pustaka yang diperlukan secara otomatis.
  3.  Jalankan sel untuk **menghubungkan (mount) Google Drive** Anda.
  4.  **PENTING:** Pastikan path file di dalam notebook sudah benar menunjuk ke lokasi data `.csv` di Drive Anda.
  5.  Jalankan semua sel untuk melatih model. Hasilnya, file-file citra klasifikasi (`.tif`) akan tersimpan di Google Drive Anda.

**3. Unggah Hasil dan Visualisasi di GEE**

- **Unggah Citra Klasifikasi:** Kembali ke GEE Code Editor. Unggah semua file `.tif` yang dihasilkan dari langkah 2 sebagai **Image Asset** baru. Catat _Asset ID_ dari setiap citra.
- **Jalankan Skrip Aplikasi Web:**
  1.  Buat satu skrip GEE terakhir untuk file `web`. Salin-tempel kodenya.
  2.  **PENTING:** Di bagian `imports` paling atas skrip `web`, **ganti semua _Asset ID_** (untuk `cnn1_ags`, `rf_jun`, dll.) dengan _Asset ID_ dari citra klasifikasi yang baru saja Anda unggah.
  3.  Klik tombol `Run`. Aplikasi web visualisasi sekarang akan berjalan di panel GEE Anda menggunakan hasil klasifikasi yang Anda buat sendiri.
