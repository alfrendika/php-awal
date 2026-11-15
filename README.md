# Lab7Web_PHP — Praktikum 7: Pemrograman Server-Side dengan PHP

| | |
|---|---|
| **Mata Kuliah** | Pemrograman Web |
| **Program Studi** | Teknik Informatika, Universitas Pelita Bangsa |
| **Nama** | Rahsya Alfrendika |
| **NIM** | 312510339 |
| **Kelas** | I253C |

## 1. Tujuan Praktikum

- Memahami perbedaan pemrosesan client-side dan server-side.
- Mengenali sintaks PHP dan menjalankan file PHP melalui server lokal.
- Menggunakan variabel, tipe data, operator, percabangan, perulangan, dan function.
- Menerima dan memproses data form HTML dengan metode GET dan POST.
- Melakukan validasi dan sanitasi input dasar sebelum data ditampilkan atau diproses.
- Membangun aplikasi sederhana yang menerima, memproses, dan menampilkan data pengguna.

## 2. Perangkat yang Digunakan

- Laptop/PC
- Web browser (Chrome/Edge/Firefox)
- Visual Studio Code (+ ekstensi PHP Intelephense)
- PHP 8.x (menggunakan built-in web server `php -S`)
- Git & GitHub

## 3. Cara Menjalankan Server Lokal

**Opsi A — PHP built-in server (disarankan, tanpa XAMPP):**

```bash
cd Lab7Web_PHP
php -S localhost:8000
```

Lalu buka <http://localhost:8000/> di browser. Hentikan server dengan `Ctrl + C`.

**Opsi B — XAMPP/Laragon:** salin folder `Lab7Web_PHP` ke `C:\xampp\htdocs\` (XAMPP) atau `C:\laragon\www\` (Laragon), jalankan Apache, lalu buka <http://localhost/Lab7Web_PHP/>.

> Jangan membuka file `.php` dengan klik ganda (`file:///...`), karena kode PHP tidak akan dieksekusi.

Langkah lengkap dari instalasi sampai commit ada di [`PANDUAN_VSCODE.md`](PANDUAN_VSCODE.md).

## 4. Struktur File

```
Lab7Web_PHP/
├── index.php                    # Latihan 1 + menu semua latihan
├── latihan2_percabangan.php     # Latihan 2: variabel, operator, percabangan
├── latihan3_array.php           # Latihan 3: perulangan dan array
├── latihan4_function.php        # Latihan 4: function
├── latihan5_get.php             # Latihan 5: form GET
├── latihan6_post.php            # Latihan 6: form POST
├── latihan7_transaksi.php       # Latihan 7: pengolahan data (subtotal)
├── mini_project.php             # Mini project: tampilan form + hasil
├── eksperimen1_rata_rata.php    # Eksperimen 1: rata-rata 3 nilai
├── eksperimen2_cari_array.php   # Eksperimen 2: cari nama (GET + array)
├── eksperimen3_rupiah.php       # Eksperimen 3: function format Rupiah
├── eksperimen4_nim.php          # Eksperimen 4: validasi NIM
├── eksperimen5_reset.php        # Eksperimen 5: tombol reset vs proses ulang
├── includes/
│   ├── header.php               # kepala HTML bersama
│   ├── footer.php               # penutup HTML bersama
│   ├── fungsi.php               # function reusable (diskon, luas, rupiah, dll.)
│   └── mahasiswa_logic.php      # logika validasi mini project (dipisah dari tampilan)
├── assets/style.css             # gaya tampilan
├── screenshots/                 # taruh screenshot hasil di sini
├── README.md
└── PANDUAN_VSCODE.md
```

## 5. Ringkasan Hasil

| Bagian | File | Ringkasan |
|---|---|---|
| Latihan 1 | `index.php` | PHP dieksekusi server; browser hanya menerima HTML. Waktu server tampil lewat `date()`. |
| Latihan 2 | `latihan2_percabangan.php` | Nilai akhir = 30% tugas + 30% UTS + 40% UAS, predikat via `if/elseif`. Diuji dengan 4 kombinasi nilai. |
| Latihan 3 | `latihan3_array.php` | Daftar 7 mahasiswa (3 nama ditambahkan) ditampilkan dengan `foreach`. |
| Latihan 4 | `latihan4_function.php` | `hitungDiskon()`, ditambah `hitungLuasPersegiPanjang()` dan `tentukanKelulusan()`. |
| Latihan 5 | `latihan5_get.php` | Data terkirim lewat URL (`?kata=...`), ditampilkan aman dengan `htmlspecialchars()`. |
| Latihan 6 | `latihan6_post.php` | Data dikirim lewat body request, divalidasi tidak kosong, output di-escape. |
| Latihan 7 | `latihan7_transaksi.php` | Validasi harga (numerik, ≥ 0) dan jumlah (bilangan bulat ≥ 1), lalu hitung subtotal. |
| Mini Project | `mini_project.php` + `includes/mahasiswa_logic.php` | Form nama, NIM, prodi, semester (1–14), email. Validasi server-side, semua error ditampilkan, hasil valid ditampilkan sebagai tabel ringkasan. |
| Eksperimen 1–5 | `eksperimen*.php` | Rata-rata nilai, pencarian array, format Rupiah, validasi NIM 10 digit angka, dan perbedaan Reset vs proses ulang server. |

### Kasus Uji Input (Mini Project)

**Input valid**

| # | Nama | NIM | Prodi | Semester | Email | Hasil |
|---|---|---|---|---|---|---|
| 1 | Andi Pratama | 2023123456 | Teknik Informatika | 5 | andi@example.com | Ringkasan data tampil |
| 2 | Siti Aminah | 2022987654 | Teknik Informatika | 14 | siti.aminah@mail.co.id | Ringkasan data tampil (batas atas semester) |

**Input tidak valid**

| # | Nama | NIM | Prodi | Semester | Email | Hasil |
|---|---|---|---|---|---|---|
| 1 | _(kosong)_ | 2023123456 | Teknik Informatika | 5 | andi@example.com | Error: "Nama wajib diisi." |
| 2 | Budi | 2023111222 | Teknik Informatika | 15 | budi@@mail | Error: semester harus 1–14 **dan** format email tidak valid |

Tambahan uji keamanan: memasukkan `<b>Halo</b>` atau tanda kutip pada nama tampil sebagai teks biasa (tidak dieksekusi) karena memakai `htmlspecialchars()`.

### Screenshot

Simpan screenshot di folder `screenshots/` lalu tampilkan di sini, contoh:

```markdown
![Latihan 1](screenshots/latihan1.png)
![Mini Project - valid](screenshots/mini_valid.png)
![Mini Project - error](screenshots/mini_error.png)
```

## 6. Jawaban Pertanyaan Evaluasi

1. **Perbedaan client-side dan server-side?**
   Client-side (HTML, CSS, JavaScript) dijalankan di browser pengguna. Server-side (PHP) dijalankan di server: menerima request, memproses input, menjalankan aturan aplikasi, lalu mengirim respons (biasanya HTML) ke browser. Browser tidak pernah melihat kode PHP mentah.

2. **Mengapa file PHP harus dijalankan lewat web server?**
   Karena PHP perlu interpreter yang dipanggil oleh web server. Jika dibuka dengan klik ganda (`file:///`), browser hanya menampilkan teks file tanpa mengeksekusi PHP. Lewat `http://localhost/`, server menjalankan PHP dan mengirim hasilnya.

3. **Fungsi tanda `$` pada variabel PHP?**
   Penanda bahwa sebuah nama adalah variabel (misal `$nama`). Nama variabel bersifat case-sensitive (`$nama` ≠ `$Nama`).

4. **Perbedaan GET dan POST?**
   GET mengirim data lewat parameter URL (terlihat di address bar, tersimpan di riwayat, ada batas panjang), cocok untuk permintaan yang tidak mengubah data seperti pencarian. POST mengirim data di body request, lazim untuk pengiriman form. POST bukan enkripsi, jadi tetap gunakan HTTPS untuk data sensitif.

5. **Mengapa input perlu divalidasi di sisi server?**
   Validasi di browser (`required`, `min`, dll.) mudah dilewati lewat DevTools atau tool seperti curl. Server tidak boleh percaya input dari luar, sehingga validasi server-side adalah pemeriksaan utama untuk menjaga data tetap benar dan aman.

6. **Fungsi `htmlspecialchars()`?**
   Mengubah karakter khusus HTML (`<`, `>`, `&`, `"`, `'`) menjadi entitas aman, sehingga input pengguna tampil sebagai teks dan tidak dieksekusi sebagai HTML/JavaScript. Ini mengurangi risiko XSS.

7. **Manfaat function?**
   Kode bisa dipakai ulang (tidak copy-paste), lebih rapi dan mudah dibaca, mudah diuji dan dirawat (perubahan cukup di satu tempat), serta memecah program menjadi bagian-bagian kecil.

## 7. Kesimpulan

PHP berjalan di sisi server dan hanya mengirim hasil (HTML) ke browser. Input dari form harus selalu divalidasi di server dan di-escape dengan `htmlspecialchars()` saat ditampilkan. Pemisahan logika pemrosesan (`includes/`) dari tampilan membuat kode lebih terstruktur.
