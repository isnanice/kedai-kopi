# Sudo Sruput - Tugas Praktik Minggu 2

Website statis Sudo Sruput merupakan proyek praktik pengembangan web menggunakan HTML5 murni tanpa CSS. Website ini terdiri dari tiga halaman utama, yaitu Beranda, Daftar Menu, dan Pemesanan, yang dirancang untuk memberikan informasi mengenai kedai kopi serta menyediakan formulir pemesanan online

## Susunan Folder
- `index.html` : Halaman beranda (sambutan, gambar suasana kedai, dan jam buka)
- `menu.html` : Daftar menu dalam kategori Kopi dan Non Kopi
- `pesan.html` : Formulir pemesanan online
- `img/suasana-sudosruput.svg` : Gambar ilustrasi suasana kedai untuk beranda
- `README.md` : Jawaban pertanyaan refleksi langkah 6


## Jawaban Langkah 6

### 6a. Apa yang muncul di address bar setelah form dikirim, dan mengapa data form tampil di sana? Hubungkan dengan materi method HTTP di Minggu 1.
Saat saya mencoba mengirim form dengan field wajib (`Nama Pemesan` atau `Nomor WhatsApp`) yang masih kosong, browser menahan pengiriman dan memunculkan pesan peringatan bawaan karena field tersebut diberi atribut `required`. Address bar tidak berubah.

Setelah semua field diisi lengkap dan tombol **Kirim** diklik, browser memuat ulang `pesan.html` dan URL di address bar berubah menjadi:
`http://127.0.0.1:5500/pesan.html?nama=Isna&wa=081234567890&menu=caffe_latte&jumlah=1&cara_ambil=ambil_di_tempat&catatan=`

Di belakang nama berkas `pesan.html`, muncul tanda tanya (`?`) yang diikuti oleh query string (parameter URL) berisi pasangan `name=value` yang dipisahkan tanda ampersand (`&`):
- Nama kunci diambil dari atribut `name` pada masing-masing elemen input, sedangkan nilainya diambil dari isian pengguna (untuk `<select>` dan `<input type="radio">`, nilai yang dikirim adalah isi atribut `value` seperti `caffe_latte` dan `ambil_di_tempat`).
- Jika isian mengandung spasi atau karakter khusus, browser mengubahnya menggunakan URL Encoding / Percent-Encoding (misalnya spasi menjadi `+` atau `%20`).
- Kolom catatan tetap ikut terkirim dengan nilai kosong (`catatan=`).

**Hubungan dengan materi HTTP Method di Minggu 1:**
Data form tampil di address bar karena elemen `<form>` menggunakan `method="get"`. Pada materi protokol HTTP Minggu 1, `GET` adalah HTTP method yang bersifat Safe dan Idempotent yang digunakan untuk meminta/mengambil sumber daya (*resource*) dari server, sehingga HTTP request dengan `GET` tidak memiliki *request body*. Karena tidak ada *body*, satu-satunya cara browser mengirimkan data isian form adalah dengan menempelkannya ke dalam query string pada URL di baris pertama HTTP request (Request Line). Sebaliknya, jika form menggunakan `method="post"`, data isian dikirim di dalam *request body* sehingga tidak muncul di address bar. Selain itu, halaman terlihat tidak berubah setelah submit karena Live Server bekerja sebagai Static Web Server yang hanya mengirimkan berkas HTML apa adanya tanpa memproses data query string tersebut.

### 6b. Pilih satu bagian halamanmu yang memakai element semantic. Mengapa kamu memilih element itu dan bukan &lt div&gt;? `<div>`
Saya memilih elemen `<nav>` yang membungkus daftar tautan ke tiga halaman (`Beranda`, `Daftar Menu`, dan `Pemesanan`) di dalam `<header>`.

Secara tampilan polos tanpa CSS, `<nav>` dan `<div>` memang terlihat sama. Namun, `<div>` hanyalah wadah generik non-semantik yang tidak memberikan informasi apa pun mengenai fungsi konten di dalamnya. Dengan memakai `<nav>`:
1. Aksesibilitas (*Screen Reader*): Browser dan teknologi asistif seperti *screen reader* langsung mengenali blok tersebut sebagai landmark navigasi utama, sehingga pengguna tunanetra bisa langsung melompat ke menu navigasi tanpa harus mendengarkan pembacaan halaman dari awal.
2. Struktur & Keterbacaan Kode: Mesin pencari (*search engine*) dapat membedakan mana tautan navigasi utama situs dan mana tautan biasa di dalam konten, serta kode HTML menjadi jauh lebih jelas dibaca tanpa menumpuk tag `<div>` (*div soup*).