# Aplikasi Penampil nama-nama Cryptocurrency - Tugas 3 PBPB

Aplikasi mobile hybrid berbasis Android yang berfungsi untuk menampilkan data harga cryptocurrency secara *real-time* dunia. Data diambil langsung dari API publik Coinlore. Proyek ini dibangun menggunakan **Ionic Framework**, **Vue.js**, **TypeScript**, dan **Vite** sebagai pembungkus proyek web, serta **Capacitor** untuk menjembatani aplikasi ke platform Android asli.

## Tampilan & Fitur Aplikasi
* **Tombol Refresh:** Berada di bagian atas untuk memperbarui data cryptocurrency terbaru dari API secara real-time.
* **Informasi Kolom:** Menampilkan atribut **Rank**, **Name** (Nama & Simbol Koin), dan **Price USD** (Harga dalam Dollar).
* **Desain Kustom:** Baris list data menggunakan warna latar belakang krem lembut (`#fef4cd`) dengan batas garis tipis yang disesuaikan agar mirip dengan mockup tugas.

## Sumber API Online
Data diambil secara *live* dari alamat:
`https://api.coinlore.net/api/tickers/`

## Prasyarat Sistem (Prerequisites)
Sebelum menjalankan proyek ini, pastikan perangkat laptop Anda telah terinstall:
* [Node.js](https://nodejs.org/) (Versi LTS direkomendasikan)
* [Android Studio](https://developer.android.com/studio) (Untuk sinkronisasi dan kompilasi ke Android SDK)

## Langkah-Langkah Menjalankan Proyek

### 1. Instalasi Dependensi
Buka terminal di dalam folder proyek ini (`cryptocurrency`), lalu jalankan perintah berikut untuk mengunduh semua library yang diperlukan:
```bash
npm install
```

### 2. Menjalankan di Browser (Development Mode)
Untuk menguji dan melihat tampilan aplikasi langsung melalui browser laptop, gunakan perintah:
```Bash
npm run dev
```
Buka alamat tautan lokal yang muncul di terminal (http://localhost:5173) dan gunakan mode inspeksi perangkat (Mobile Toggle / F12) pada browser.

### 3. Kompilasi & Sinkronisasi ke Platform Android
Jika Anda melakukan perubahan pada kode utama (di dalam folder src/), lakukan kompilasi ulang kode web dan sinkronisasikan ke folder Android dengan perintah:
```Bash
npm run build
npx cap sync
```

### 4. Menjalankan Aplikasi di HP Android asli
**Cara A**: Menggunakan Android Studio (Sangat Direkomendasikan)
* Buka folder proyek bagian /android menggunakan Android Studio.
* Hubungkan HP Android ke laptop menggunakan kabel USB (Pastikan fitur USB Debugging dan Install via USB sudah aktif di Opsi Pengembang HP).
* Klik tombol Segitiga Hijau (Run App) di bagian kanan atas toolbar Android Studio.

**Cara B**: Mengambil File APK Mentah.
* Jika kompilasi berhasil, Anda juga dapat mengambil file aplikasi siap pakai (debug binary) langsung dari direktori laptop di bawah ini untuk dikirim ke HP via WhatsApp/Drive:
android/app/build/intermediates/apk/debug/app-debug.apk

Struktur Folder Utama
* **src/views/HomePage.vue** - Berisi template UI, logika fetching API, dan styling kotak krem aplikasi.
* **src/App.vue** - Komponen akar utama aplikasi.
* **android/** - Folder native Android yang dihasilkan oleh Capacitor CLI.
