## 📝 Identitas Mahasiswa

Berikut adalah data identitas pengembang proyek UAS Pemrograman Web 2:

| Informasi | Detail |
| :--- | :--- |
| **Nama** | Zahrah Amanda Fauziyah |
| **NIM** | 312410193 |
| **Kelas** | I.24.1.B |
| **Mata Kuliah** | Pemrograman Web 2 |
| **Dosen Pengampu** | Agung Nugroho, S.Kom., M.Kom |
| **Universitas** | Universitas Pelita Bangsa |

## 🗄️ Skema Relasi Database (Database Schema)

Berikut adalah visualisasi rancangan basis data sistem **E-Inventory** yang terdiri dari 5 tabel utama yang saling berelasi pada phpMyAdmin Designer:

<img width="1408" height="768" alt="database" src="https://github.com/user-attachments/assets/611221b8-f07c-4767-bd2d-9afd4884535e" />


### 1. Struktur dan Entitas Tabel

*   **`users`**: Menyimpan data autentikasi pengguna/administrator sistem.
    *   `id`: Primary key (Auto Increment) untuk identitas unik user.
    *   `nama`, `email`, `password`: Menyimpan data kredensial akun log-in admin.
*   **`kategori`**: Mengelompokkan jenis-jenis barang inventaris.
    *   `id`: Primary key dari entitas kategori.
    *   `nama_kategori`: Label klasifikasi barang (contoh: Alat Tulis, Elektronik, dll).
*   **`supplier`**: Menyimpan data mitra eksternal atau vendor penyedia pasokan gudang.
    *   `id`: Primary key dari entitas entitas supplier.
    *   `nama_perusahaan`, `email`, `telepon`, `alamat`: Informasi kontak lengkap vendor.
*   **`barang`**: Tabel master operasional yang menampung seluruh aset komoditas inventaris.
    *   `id`: Primary key dari entitas barang.
    *   `nama_barang`, `stok`, `harga`: Detail data fisik dan nominal aset.
    *   `kategori_id` & `supplier_id`: Foreign key penhubung entitas relasi.
*   **`histori`**: Mencatat log sirkulasi barang masuk dan barang keluar secara berkala.
    *   `id`: Primary key log transaksi.
    *   `tanggal`, `tipe`, `jumlah`: Data kronologis aktivitas logistik.
    *   `barang_id`: Foreign key pengikat aktivitas terhadap objek barang spesifik.

---

### 🔗 Kardinalitas Relasi Antar Tabel

Berdasarkan garis relasi (*Foreign Key Constraints*) pada skema di atas, hubungan antartabel dikonfigurasi sebagai berikut:

1.  **Relasi `kategori` Ke `barang` (`One-to-Many`)**:
    *   Satu baris kategori dapat menampung banyak (*Many*) data produk barang. 
    *   Relasi diikat oleh Foreign Key `kategori_id` pada tabel `barang` yang merujuk ke Primary Key `id` pada tabel `kategori`.
2.  **Relasi `supplier` Ke `barang` (`One-to-Many`)**:
    *   Satu perusahaan supplier dapat menyuplai banyak jenis barang ke gudang penyimpanan.
    *   Relasi diikat oleh Foreign Key `supplier_id` pada tabel `barang` yang merujuk ke Primary Key `id` pada tabel `supplier`.
3.  **Relasi `barang` Ke `histori` (`One-to-Many`)**:
    *   Satu item barang yang sama dapat memiliki banyak rekam jejak riwayat mutasi logistik (berulang kali masuk gudang maupun keluar gudang).
    *   Relasi diikat oleh Foreign Key `barang_id` pada tabel `histori` yang merujuk ke Primary Key `id` pada tabel `barang`.
  
## 🖥️ Dokumentasi Antarmuka Aplikasi (User Interface Showcase)

Berikut adalah dokumentasi visual dari modul-modul antarmuka (*Frontend Client*) yang dibangun menggunakan kerangka kerja modern, terintegrasi langsung ke RESTful API Backend secara real-time.

---

### 1. Halaman Utama / Landing Page (Guest View)
Bagian beranda awal yang diakses oleh pengguna umum sebelum masuk ke sistem penatausahaan.

*   **Header & Statistik Ringkas**
  <img width="938" height="439" alt="Cuplikan layar 2026-06-19 192912" src="https://github.com/user-attachments/assets/362a1b56-7151-4727-a062-50e6d873211f" />

    Menampilkan *Value Proposition* utama sistem E-Inventory, tombol navigasi cepat, serta komponen *Card* yang menyajikan ringkasan akumulasi data (Barang, Kategori, Supplier, Transaksi) secara transparan.
*   **Grid Fitur Unggulan**
  <img width="934" height="366" alt="Cuplikan layar 2026-06-19 192924" src="https://github.com/user-attachments/assets/f0101eb5-b486-4189-9fda-4ec0a6c0269b" />

    Edukasi visual mengenai 6 pilar fungsionalitas utama sistem yang dapat dioperasikan oleh administrator setelah melewati proses otentikasi.
*   **Profil Pengembang / Developer Section**
  <img width="934" height="430" alt="Cuplikan layar 2026-06-19 192935" src="https://github.com/user-attachments/assets/107f909d-bbd5-47b0-8598-24b951070ff9" />

    Halaman identitas akademik yang memuat nama pengembang (Zahrah Amanda Fauziyah), NIM, Program Studi Teknik Informatika, dan Universitas Pelita Bangsa sebagai bentuk pemenuhan orisinalitas proyek UAS Pemrograman Web 2.

---

### 2. Gerbang Otentikasi / Login Page
*   **Form Login Komponen**
  <img width="280" height="362" alt="Cuplikan layar 2026-06-19 194013" src="https://github.com/user-attachments/assets/d9ee603c-1ff0-4a90-a60c-60bac07f6806" />

    Antarmuka bersih (*clean UI*) untuk proses masuk administrator. Dilengkapi fitur keamanan interaktif seperti *Toggle visibility password* (sembunyi/lihat sandi), opsi *Remember Me*, dan validasi input berbasis email sebelum data dikirim ke endpoint otentikasi JWT/Bearer Token.

---

### 3. Panel Utama / Admin Dashboard
*   **Dashboard Statistik & Grafik**
  <img width="928" height="418" alt="Cuplikan layar 2026-06-19 194049" src="https://github.com/user-attachments/assets/9c0837d7-1945-43af-a28b-9f0016fd77cb" />

    Pusat kendali utama administrator setelah sukses login. Menyajikan *Metrik Ringkas* (Total Barang, Kategori, Supplier, Barang Keluar) dan *Chart visualisasi sirkulasi logistik* berbasis grafik batang untuk mempermudah pemantauan arus barang masuk secara periodik.

---

### 4. Modul Manajemen Data Master & Transaksi (CRUD Modal)
Seluruh operasi manipulasi data menggunakan pendekatan *Single Page Application* (SPA) dengan memanfaatkan komponen **Modal Form Pop-Up** yang dinamis tanpa memicu *reload* halaman penuh.

*   **Tambah Data Master Barang**
  <img width="944" height="392" alt="Cuplikan layar 2026-06-19 194309" src="https://github.com/user-attachments/assets/f8e815f7-f494-440f-b345-82586308e237" />

    Formulir modal untuk mencatat komoditas baru. Mengintegrasikan input relasional berupa pilihan *Dropdown* Kategori dan Supplier yang datanya diambil langsung dari tabel master lain (Foreign Key Constraints).
*   **Tambah Kategori Barang**
  <img width="944" height="391" alt="Cuplikan layar 2026-06-19 194326" src="https://github.com/user-attachments/assets/f999d9d0-775d-4665-9386-f43f658cfdc3" />

    Antarmuka minimalis khusus untuk memperluas klasifikasi atau segmentasi jenis inventaris (contoh penambahan: TV, Skincare).
*   **Tambah Vendor / Supplier**
  <img width="943" height="416" alt="Cuplikan layar 2026-06-19 194349" src="https://github.com/user-attachments/assets/c6bb7c73-57da-4450-8729-fdb5a6c163c6" />

    Form modal terpusat untuk merekam data mitra penyuplai baru, mencakup nama perusahaan, email kontak, nomor telepon operasional, dan alamat fisik vendor.
*   **Pencatatan Histori Logistik**
  <img width="944" height="437" alt="Cuplikan layar 2026-06-19 194431" src="https://github.com/user-attachments/assets/72203d83-438f-4d33-8609-8de50f34862a" />

    Formulir mutasi sirkulasi barang. Berfungsi mencatat secara kronologis apakah suatu barang mengalami aktivitas "Barang Masuk" atau "Barang Keluar" lengkap dengan penentuan tanggal dan kuantitas (jumlah) barang.

---

### 5. Manajemen Akun / Administrator Profile
*   **Halaman Profil & Metrik Pengguna**
  <img width="934" height="436" alt="Cuplikan layar 2026-06-19 194448" src="https://github.com/user-attachments/assets/3381c89a-7cec-4901-8d25-e97828fa676f" />

    Memuat informasi kredensial personal dari pengguna yang sedang aktif (Zahrah Amanda Fauziyah - Role: Administrator). Halaman ini juga merangkum kembali kontribusi data yang dikelola pengguna, deskripsi proyek UAS, serta indikator *Skill Development* (HTML, CSS, JavaScript/Vue) di bagian bawah halaman.

## 🚀 Panduan Instalasi & Demo Aplikasi

Anda dapat mengakses versi demo aplikasi secara online melalui tautan berikut:
👉 **[Klik di sini untuk Demo E-Inventory](https://project-uas-pem-web-2-zahrah.netlify.app/)**

Jika Anda ingin menjalankan sistem di lingkungan lokal (*development mode*), pastikan **PHP**, **Composer**, dan **Node.js** sudah terinstal, lalu ikuti langkah berikut:

### 1. Backend (CodeIgniter 4 API)
1. Buka terminal di folder `backend-api/`.
2. Instal dependensi: `composer install`.
3. Salin `.env.example` ke `.env` dan atur konfigurasi database lokal Anda.
4. Jalankan server: `php spark serve` (Akan berjalan di `http://localhost:8080`).

### 2. Frontend (VueJS 3)
1. Buka terminal di folder `frontend-spa/`.
2. Pastikan file konfigurasi Axios sudah mengarah ke `http://localhost:8080/api/`.
3. Jalankan aplikasi dengan server lokal (misalnya menggunakan *Live Server* VS Code atau `python -m http.server 3000`).

---
*Catatan: Pastikan konfigurasi CORS pada backend sudah diaktifkan agar frontend dapat berkomunikasi dengan API.*

**Link Demo Aplikasi**
**https://project-uas-pem-web-2-zahrah.netlify.app/**
