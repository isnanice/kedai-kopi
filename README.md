Repository: https://github.com/isnanice/kedai-kopi.git

# Sudo Sruput - Tugas Praktik Minggu 3

Website kedai kopi Sudo Sruput yang dikembangkan dari hasil praktik Minggu 2 dengan menerapkan CSS untuk mengatur tampilan halaman. Ketiga halaman menggunakan satu berkas CSS eksternal, yaitu `css/style.css`. Pengaturan tampilan menggunakan Flexbox, CSS Grid, serta media query dengan pendekatan mobile first agar website dapat menyesuaikan ukuran layar smartphone maupun laptop.

## Jawaban Pertanyaan Tugas 8 (Minggu 3)

### Pertanyaan A

> **Sebutkan satu bagian yang kamu susun dengan Flexbox dan satu bagian dengan Grid. Mengapa pilihan itu cocok untuk kedua bagian tersebut?**

**Jawaban:**

Dalam website Sudo Sruput, saya menggunakan Flexbox pada bagian header dan navigasi, sedangkan CSS Grid digunakan untuk menyusun card menu pada halaman `menu.html`.

1. **Bagian yang menggunakan Flexbox: Header dan Navigasi**

   Flexbox digunakan untuk mengatur posisi nama kedai dan navigasi yang terdapat pada bagian `<header>`. Saya memilih Flexbox karena tata letak header hanya membutuhkan pengaturan dalam satu arah, yaitu secara horizontal atau vertikal.

   - Pada layar ponsel, saya menggunakan `flex-direction: column` agar nama kedai dan navigasi tersusun ke bawah.
   - Pada layar tablet dan laptop dengan lebar minimal 600px, saya menggunakan `flex-direction: row` dan `justify-content: space-between` agar nama kedai berada di sebelah kiri dan navigasi berada di sebelah kanan.

   Flexbox cocok digunakan karena memudahkan pengaturan posisi dan jarak antarelemen tanpa harus menentukan posisi masing-masing secara manual.

2. **Bagian yang menggunakan CSS Grid: Card Menu**

   CSS Grid digunakan pada bagian daftar menu di halaman `menu.html`, khususnya untuk mengatur kumpulan card minuman. Saya memilih Grid karena tata letak menu membutuhkan pengaturan baris dan kolom secara bersamaan.

   Pengaturan kolom disesuaikan dengan ukuran layar menggunakan media query:

   - Layar ponsel: satu kolom menggunakan `grid-template-columns: 1fr`.
   - Layar dengan lebar minimal 600px: dua kolom menggunakan `repeat(2, 1fr)`.
   - Layar dengan lebar minimal 960px: tiga kolom menggunakan `repeat(3, 1fr)`.

   Grid cocok digunakan karena setiap card dapat tersusun secara teratur dengan jarak yang sama melalui properti `gap`. Dengan begitu, tampilan daftar menu tetap rapi meskipun ukuran layar berubah.

---

### Pertanyaan B

> **Ceritakan satu aturan CSS yang awalnya tidak berlaku. Apa yang kamu lihat di panel Styles, dan bagaimana kamu memperbaikinya?**

**Jawaban:**

Aturan CSS yang awalnya tidak berlaku adalah `margin-bottom: 1.25rem` pada selector `form p`, ketika diterapkan ke paragraf yang berisi pilihan radio di dalam `<fieldset>` pada halaman `pesan.html`.

1. **Aturan CSS yang terlibat:**

   ```css
   form p {
       margin-bottom: 1.25rem;
   }

   fieldset p {
       margin-bottom: 0.5rem;
   }
   ```

2. **Yang terlihat di panel Styles:**

   Saya membuka Developer Tools dengan F12, memilih tab Elements, lalu memeriksa salah satu `<p>` di dalam `fieldset` melalui panel Styles. Di sana, aturan `form p { margin-bottom: 1.25rem }` tampil **dicoret**, sedangkan aturan `fieldset p { margin-bottom: 0.5rem }` yang aktif. Nilai margin sebenarnya juga bisa saya cek di tab Computed.

3. **Penyebab dan cara memperbaikinya:**

   Kedua selector sama-sama terdiri dari dua element, sehingga specificity-nya sama, yaitu `0,0,2`. Karena specificity-nya seri, browser memakai aturan yang **ditulis paling akhir** di `style.css`, yaitu `fieldset p`. Jadi aturan `form p` kalah bukan karena salah tulis, tetapi karena kalah urutan.

   Untuk memastikan hal ini, saya mencoba memindahkan `fieldset p` ke atas `form p`, dan hasilnya terbalik: aturan `form p` yang menang. Karena jarak antar pilihan radio memang sebaiknya lebih rapat dibanding jarak antar field lainnya, saya mengembalikan `fieldset p` ke posisi setelah `form p`. Dengan urutan itu, field biasa memakai margin 1.25rem, sedangkan pilihan radio di dalam fieldset memakai margin 0.5rem.

---

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