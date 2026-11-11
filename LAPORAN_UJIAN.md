# Laporan UTS Web Software Tools

**Nama: Maura Mutiara Maheta**
**Nomor Induk Mahasiswa: 12523021**
**Kelas: A**
**Tanggal: 11 November 2026**

## Catatan kondisi awal (sebelum perbaikan)
- Aplikasi berhasil dibuka di `http://localhost:5057`.
- Daftar produk tidak tampil. Network menunjukkan request `GET /api/barang` gagal dengan status `404`; Console menampilkan `Permintaan gagal dengan status 404` dan status halaman `Gagal memuat produk`.
- Keranjang awal menunjukkan `0 barang` dan total `Rp 0`. Tombol tambah belum dapat diuji dari UI karena produk tidak berhasil ditampilkan.
- Commit awal yang tersedia: `7620011 uts_wst` (`main`/`origin/main`). Belum ada perubahan kode perbaikan.

## A. Bukti pemeriksaan masalah
| Masalah | Alat yang digunakan | Bukti pemeriksaan | Perkiraan penyebab | Perbaikan | Hasil setelah perbaikan |
|---|---|---|---|---|---|
| Produk | Network, Console | Sebelum: `GET /api/barang` berstatus `404`. Sesudah: katalog memuat 4 produk. | Frontend meminta endpoint yang berbeda dari endpoint yang disediakan server (`/api/products`). | Mengubah request frontend ke `/api/products`. | 4 produk tampil dan status halaman menunjukkan `4 produk tersedia`. |
| Tombol keranjang | Elements, pemeriksaan kode, browser | Sebelum: tombol tidak bereaksi; kelas tombol `.add-button` tidak cocok dengan selector listener `.add-to-cart`. Sesudah: dua klik menambah `2 barang`. | Handler tidak pernah dipasang ke tombol yang dirender. | Menyamakan selector listener menjadi `.add-button`. | Klik tombol menambah barang; dua klik Mouse Nirkabel menampilkan jumlah 2. |
| Total belanja | Pengujian otomatis, browser | Sebelum: `5/7` test lulus; kuantitas 2 menghasilkan `75.000` (harus `150.000`) dan kuantitas campuran menghasilkan `225.000` (harus `600.000`). Sesudah: `7/7` lulus; browser menampilkan `Rp 150.000` untuk 2 Mouse Nirkabel. | Fungsi menjumlahkan harga satuan tanpa mengalikannya dengan kuantitas. | Menghitung `item.price * item.quantity` untuk setiap item. | Semua test lulus; total browser sesuai harga dikali jumlah. |

## B. Hasil pengujian
- Jumlah pengujian sebelum perbaikan: 5 berhasil, 2 gagal (dari 7).
- Jumlah pengujian berhasil setelah perbaikan: 7 berhasil, 0 gagal (dari 7).
- Catatan perubahan pada fungsi yang diperiksa: `addProduct` tetap menambah kuantitas produk yang sama; `calculateTotal` kini mengalikan harga dengan kuantitas.

## C. Kualitas kode
- Temuan sebelum perbaikan: `npm run lint` lulus; `format:check` dan `quality:check` meminta format ulang pada `public/app.js`.
- Perbaikan yang dilakukan: menjalankan formatter Biome pada `public/app.js` dan `src/cart.js`.
- Hasil pemeriksaan ulang: `npm run lint`, `npm run format:check`, dan `npm run quality:check` semuanya lulus.

## D. Git
- Branch (jika membuat): `main` (tracking `origin/main`).
- Ringkasan commit: baseline `7620011 uts_wst`; perbaikan `fix: repair shop behavior`.
- Hasil pemeriksaan `git status`: bersih setelah commit perbaikan.

## E. Pemakaian kecerdasan buatan (jika digunakan)
- Nama alat: GitHub Copilot.
- Pertanyaan/instruksi yang diberikan: membantu mengerjakan ujian mini toko sesuai aturan, mencatat kondisi awal, lalu mencari dan memperbaiki masalah daftar produk, tombol keranjang, dan total.
- Bagian jawaban yang diterapkan: menyamakan endpoint katalog dan selector tombol; menghitung total berdasarkan harga dan kuantitas.
- Cara memeriksa apakah saran tersebut benar: memeriksa kode server/frontend, menjalankan `npm run test:once` (7/7 lulus), dan menguji katalog serta penambahan dua barang di browser.

## F. Refleksi singkat
- Satu pelajaran paling penting dari ujian ini: gunakan bukti dari Network, Console, dan test untuk membedakan masalah endpoint, event handler, dan perhitungan.
