# **Deteksi dan Pemetaan Tumbuhan Asing Invasif Eceng Gondok dengan Citra Satelit dan Machine Learning**

## **Deskripsi Proyek**

Proyek ini bertujuan untuk mendeteksi dan memetakan tumbuhan asing invasif, khususnya Eceng Gondok (Eichhornia crassipes), dengan menggunakan citra satelit dan teknik machine learning. Skripsi ini mencakup pemanfaatan data citra satelit Sentinel-1 dan Sentinel-2 serta platform Google Earth Engine (GEE) dan Google Colab untuk memproses data dan membangun model deteksi.

## **Struktur Folder**

```
├── aset
├── agustus
├── juli
├── juni
├── skripsi_eceng.ipynb
├── web
```

- **aset**: Folder ini berisi data aset yang digunakan dalam proyek, seperti shp, citra satelit dan data lainnya.
- **agustus/juni/juli**: File ini berisi kode Earth Engine Script untuk masing2 waktu (kode relatif mirip).

## **Pengerjaan Platform**

Proyek ini dilakukan menggunakan dua platform utama:

1. **Google Earth Engine (GEE)**: Untuk pengolahan citra satelit dan pembuatan web apps.
2. **Google Colab**: Untuk melakukan training model, pengolahan data, serta ekspor hasil dari GEE.

## **Cara Penggunaan (Reproducibility)**

### **1. Pengumpulan data menggunakan Google Earth Engine**

Skrip di GEE terdiri dari dua file utama:

- **[bulan]**: Berisi kode untuk pembuatan geometry (titik) yang digunakan sebagai sampel kelas (Eceng Gondok, air, tumbuhan lain, tanah, KJA, lainnya), serta pengimporan aset lainnya dan pengambilan serta ekspor citra ke drive.
- **web**: Berisi kode web apps dari proyek untuk menampilan visualisasi hasil pengolahan.

#### Langkah-langkah Penggunaan:

1. Modifikasi `assetId` (wajib) dan `folder` (opsional) pada bagian `export toAsset` sesuai dengan kebutuhan.
2. Jalankan skrip di GEE.
3. Pastikan semua task (proses ekspor, perhitungan, dan lainnya) telah selesai dijalankan dengan sukses.

#### Link Skrip GEE:

[Klik untuk mengakses skrip GEE](https://code.earthengine.google.com/?accept_repo=users/222111840/skripsi_eceng_gondok)

### **2. Pengolahan menggunakan Google Colab**

Untuk menggunakan file skripsi di Google Colab, lakukan langkah-langkah berikut:

1. Upload file `skripsi_eceng.ipynb` ke Google Colab.
2. Edit bagian `ee.Initialize(project='ee-222111840')` sesuai dengan nama proyekmu di GEE.
3. Jika ada perubahan folder saat ekspor di GEE, pastikan untuk mengganti path folder Google Drive di kode Google Colab.
4. Jalankan semua cell dengan memilih "Run All".

### **3. Web Apps**

1. Import hasil pengolahan berupa ke aset google earth, sesuaikan nama file aset pada kode
2. Jalankan kode web.js
3. (opsional) Publish web apps [[petunjuk]](https://developers.google.com/earth-engine/tutorials/community/creating-web-apps)

## **Labeling**

Proses pelabelan dilakukan dengan bantuan citra satelit terbaru (2025), dengan timestamp berikut:

- **Citra Sentinel-2**: 7/26/2024
- **Citra Sentinel-1**: 7/25/2024

Selain itu, proses pelabelan juga dibantu dengan data ortofoto dan foto/video drone dari BBWS Pemali-Juana untuk memastikan akurasi label.

#### Link Aset Ortofoto dan Foto/Video Drone:

[Klik untuk mengakses aset ortofoto dan foto/video drone](https://s.stis.ac.id/DriveSkripsiEceng)

## Mempercepat Pengolahan Menggunakan GPU (Opsional)

Untuk mempercepat pengolahan disarankan memakai GPU untuk tensorflow:

## **Persyaratan**

- **Google Earth Engine Account**: Diperlukan akun Google untuk mengakses dan menjalankan skrip di Google Earth Engine.
- **Google Colab Account**: Diperlukan akun Google untuk menggunakan Google Colab.
- **Python**: Diperlukan python pada perangkat jika ingin menjalankan secara lokal.
- **pengetahuan dasar jupyter notebook, python, tensorflow, cuda-toolkit & wsl (opsional)**

## **Pembatasan**

- Hati-hati saat melakukan pelabelan karena adanya perbedaan antara citra yang digunakan untuk pelabelan dan citra yang tersedia di Google Earth Pro.

## **Kontribusi**

Jika Anda tertarik untuk berkontribusi pada proyek ini, Anda dapat mengajukan pull request atau memberikan masukan terkait pengolahan data dan metode machine learning yang digunakan.

## **Lisensi**

Proyek ini berlisensi [Lisensi MIT](https://opensource.org/licenses/MIT).

---

Jika ada pertanyaan lebih lanjut, jangan ragu untuk menghubungi penulis melalui [email](mailto:222111840@stis.ac.id) atau forum diskusi terkait proyek ini.
