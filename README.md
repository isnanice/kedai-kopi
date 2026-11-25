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
 
Website statis untuk kedai kopi fiktif Sudo Sruput, dibuat dengan HTML saja.
 
Isi folder:
- `index.html` : Halaman beranda (sambutan, gambar, jam buka)
- `menu.html` : Daftar menu (kategori Kopi dan Non Kopi)
- `pesan.html` : Formulir pemesanan
- `img/kopi.svg` : Berkas gambar pendukung beranda
- `README.md` : Jawaban refleksi dan evaluasi tugas


## Jawaban Pertanyaan Refleksi (Langkah 6)


### Pertanyaan A
> **Apa yang muncul di address bar setelah form dikirim, dan mengapa data form tampil di sana? Hubungkan dengan materi method HTTP di Minggu 1.**


**Jawaban:**
1. **Apa yang muncul di address bar:**  
   Setelah menekan tombol "Kirim Pemesanan", URL pada *address bar* browser berubah. Di belakang nama file target (`pesan.html`), muncul karakter tanda tanya (`?`) yang diikuti oleh serangkaian pasangan nama atribut input dan nilai isian (*key-value pair*) yang dipisahkan oleh karakter ampersand (`&`). Bentuk ini dikenal sebagai **query string**.  
   
   *Contoh tampilan di address bar:*
   ```text
   pesan.html?nama=Budi+Santoso&wa=08123456789&menu=kopi_susu_aren&jumlah=2&cara_ambil=ambil_di_tempat&catatan=Kurangi+es
   ```
   Karakter spasi secara otomatis diubah menjadi tanda tambah (`+`) atau kode heksadesimal `%20` melalui mekanisme *URL Encoding / Percent-Encoding*.


2. **Mengapa data form tampil di sana (Hubungan dengan Method HTTP):**  
   - Pada form di `pesan.html`, kita mendefinisikan atribut `method="get"`.
   - Berdasarkan materi dasar protokol HTTP di Minggu 1, metode `GET` digunakan secara semantik untuk **meminta atau mengambil (*retrieve*) resource dari server**, bukan untuk menyimpan atau mengubah status resource di server secara permanen.
   - Sesuai spesifikasi protokol HTTP, sebuah HTTP request yang menggunakan metode `GET` **tidak memiliki *request body*** (atau *body*-nya kosong). Oleh karena itu, satu-satunya cara browser dapat mengirimkan parameter atau input formulir kepada server adalah dengan menempelkannya langsung ke dalam baris URI permintaan (*Request-URI*) di baris pertama request HTTP (*Request Line*), yaitu melalui *query string*.
   - Sebaliknya, jika form menggunakan atribut `method="post"`, data formulir akan dikemas dan disembunyikan di dalam *request body* (dengan header `Content-Type: application/x-www-form-urlencoded` atau `multipart/form-data`), sehingga data tersebut tidak terpampang secara kasat mata pada address bar browser.


---


### Pertanyaan B
> **Pilih satu bagian halamanmu yang memakai element semantic. Mengapa kamu memilih element itu dan bukan `<div>`?**


**Jawaban:**
Bagian yang saya pilih adalah elemen **`<nav>`** yang membungkus daftar tautan navigasi utama website pada bagian `<header>` di ketiga halaman (`index.html`, `menu.html`, dan `pesan.html`):


```html
<nav>
  <ul>
    <li><a href="index.html">Beranda</a></li>
    <li><a href="menu.html">Daftar Menu</a></li>
    <li><a href="pesan.html">Pemesanan</a></li>
  </ul>
</nav>
```


**Alasan memilih `<nav>` dan bukan `<div>`:**


1. **Memberikan Makna Semantik yang Jelas (*Meaning and Semantics*):**  
   Tag `<div>` adalah elemen pembungkus generik non-semantik (*non-semantic division container*). Tag `<div>` sama sekali tidak memberi tahu browser, peramban mesin pencari, maupun manusia tentang apa peran konten di dalamnya. Sebaliknya, elemen `<nav>` secara eksplisit menyatakan bahwa blok tersebut berisi **tautan navigasi utama** untuk menjelajahi situs web.


2. **Aksesibilitas dan Teknologi Asistif (*Web Accessibility / a11y*):**  
   Elemen `<nav>` secara bawaan (*native*) memiliki peran landmark ARIA (`role="navigation"`). Pengguna penyandang disabilitas netra yang menggunakan *screen reader* (seperti NVDA, JAWS, atau VoiceOver) dapat memanfaatkan tombol pintas navigasi untuk langsung melompat (*jump to landmark*) ke menu navigasi tanpa harus mendengarkan pembacaan elemen pembuka lainnya dari awal baris demi baris. Jika kita hanya memakai `<div>`, screen reader memperlakukannya sebagai blok teks biasa, sehingga navigasi menjadi jauh lebih sulit diakses.


3. **Optimasi Mesin Pencari (*Search Engine Optimization / SEO*):**  
   Mesin pencari seperti Googlebot membaca dokumen HTML untuk memahami struktur dan hierarki sebuah situs web. Dengan menandai tautan menggunakan `<nav>`, web crawler dapat mengenali arsitektur halaman dengan tepat dan membedakan antara tautan navigasi utama situs dengan tautan sekunder atau tautan konten biasa.


4. **Keterbacaan dan Kemudahan Perawatan Kode (*Maintainability*):**  
   Menggunakan elemen semantik seperti `<header>`, `<nav>`, `<main>`, `<section>`, dan `<footer>` mencegah terjadinya *“div soup”* (tumpukan tag `<div>` bersarang tanpa makna). Kode HTML menjadi jauh lebih rapi, terstruktur secara logis, dan mudah dipahami oleh pengembang lain saat bekerja dalam tim.