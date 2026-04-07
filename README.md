# Lab7Web-Semester4


# PRAKTIUM 1


**Persiapan**
# Praktikum 1: PHP Framework (Codeigniter)

## Tujuan
1. Mahasiswa mampu memahami konsep dasar Framework.
2. Mahasiswa mampu memahami konsep dasar MVC.
3. Mahasiswa mampu membuat program sederhana menggunakan Framework Codeigniter 4.

## Instruksi Praktikum
1. Persiapkan text editor misalnya VSCode.
2. Buat folder baru dengan nama **lab11_ci** pada docroot webserver (htdocs).
3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya.

---

## Langkah-langkah Praktikum

### 1. Persiapan
Sebelum memulai menggunakan Framework Codeigniter, perlu dilakukan konfigurasi pada webserver. Beberapa ekstensi PHP perlu diaktifkan untuk kebutuhan pengembangan Codeigniter 4.

Berikut beberapa ekstensi yang perlu diaktifkan:
- **php-json** ekstension untuk bekerja dengan JSON
- **php-mysqlnd** native driver untuk MySQL
- **php-xml** ekstension untuk bekerja dengan XML
- **php-intl** ekstensi untuk membuat aplikasi multibahasa
- **libcurl** (opsional), jika ingin pakai Curl

Untuk mengaktifkan ekstensi tersebut, melalui **XAMPP Control Panel**, pada bagian Apache klik **Config -> PHP.ini**

<img width="1115" height="645" alt="image" src="https://github.com/user-attachments/assets/e8ba8d46-1a25-4032-9fc2-628af1d4bee7" />


Pada bagian extension, hilangkan tanda ; (titik koma) pada ekstensi yang akan diaktifkan. Kemudian simpan kembali filenya dan restart Apache web server.

> 📸 **[Screenshot: Tampilan file PHP.ini dengan ekstensi yang sudah diaktifkan]**

---

### 2. Instalasi Codeigniter 4
Untuk melakukan instalasi Codeigniter 4 dapat dilakukan dengan dua cara, yaitu cara manual dan menggunakan composer. Pada praktikum ini kita menggunakan cara manual.

- Unduh **Codeigniter** dari website https://codeigniter.com/download
- Extrak file zip Codeigniter ke direktori **htdocs/lab11_ci**
- Ubah nama direktori **framework-4.x.xx** menjadi **ci4**
- Buka browser dengan alamat http://localhost/lab11_ci/ci4/public/

> 📸 **[Screenshot: Tampilan halaman Welcome to CodeIgniter 4 di browser]**

---

### 3. Menjalankan CLI (Command Line Interface)
Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk mengakses CLI buka terminal/command prompt.

Arahkan lokasi direktori sesuai dengan direktori kerja project dibuat **(xampp/htdocs/lab11_ci/ci4/)**

Perintah yang dapat dijalankan untuk memanggil CLI Codeigniter adalah:

```
php spark
```

> 📸 **[Screenshot: Tampilan CLI CodeIgniter setelah menjalankan perintah php spark]**

---

### 4. Mengaktifkan Mode Debugging
Codeigniter 4 menyediakan fitur **debugging** untuk memudahkan developer untuk mengetahui pesan error apabila terjadi kesalahan dalam membuat kode program.

Secara default fitur ini belum aktif. Ketika terjadi error pada aplikasi akan ditampilkan pesan kesalahan **"Whoops!"** yang tidak informatif.

> 📸 **[Screenshot: Tampilan error Whoops! sebelum mode debugging diaktifkan]**

Untuk mengaktifkan mode debugging:
- Ubah nama file **env** menjadi **.env**
- Buka file tersebut dan ubah nilai variable **CI_ENVIRONMENT** menjadi **development**

```
CI_ENVIRONMENT = development
```

> 📸 **[Screenshot: Tampilan file .env dengan CI_ENVIRONMENT = development]**

Setelah mode debugging aktif, pesan error akan ditampilkan lebih detail seperti **ParseError** beserta nama file dan nomor baris yang menyebabkan error.

> 📸 **[Screenshot: Tampilan ParseError setelah mode debugging diaktifkan]**

---

### 5. Struktur Direktori
Untuk lebih memahami Framework Codeigniter 4 perlu mengetahui struktur direktori dan file yang ada. Buka pada **Windows Explorer** atau dari **Visual Studio Code -> Open Folder**.

> 📸 **[Screenshot: Tampilan struktur direktori CI4 di VSCode atau Windows Explorer]**

Terdapat beberapa direktori dan file yang perlu dipahami fungsi dan kegunaannya:

- **.github** - folder untuk konfigurasi repo github
- **app** - folder yang berisi kode dari aplikasi yang dikembangkan
- **public** - folder yang berisi file yang bisa diakses oleh publik
- **tests** - folder yang berisi kode untuk melakukan testing dengan PHPunit
- **vendor** - folder yang berisi library yang dibutuhkan oleh aplikasi
- **writable** - folder yang berisi file yang ditulis oleh aplikasi

Sedangkan file-file yang berada pada root direktori CI:
- **.env** - file yang berisi variabel environment
- **.gitignore** - file yang berisi daftar nama file dan folder yang diabaikan Git
- **composer.json** - file JSON yang berisi informasi tentang proyek
- **spark** - program untuk menjalankan server, generate kode, dll

---

### 6. Memahami Konsep MVC
Codeigniter menggunakan konsep MVC (**Model-View-Controller**). MVC merupakan konsep arsitektur yang umum digunakan dalam pengembangan aplikasi. Konsep MVC adalah memisahkan kode program berdasarkan logic proses, data, dan tampilan.

- **Model** - kode program yang berisi pemodelan data (database atau sumber lainnya)
- **View** - kode program yang menangani tampilan user interface
- **Controller** - kode program yang berkaitan dengan logic proses yang menghubungkan antara view dan model

---

### 7. Routing dan Controller
Routing merupakan proses yang mengatur arah atau rute dari request untuk menentukan fungsi/bagian mana yang akan memproses request tersebut.

Router terletak pada file **app/Config/Routes.php**

Contoh route untuk halaman home:
```php
$routes->get('/', 'Home::index');
```

#### Membuat Route Baru
Tambahkan kode berikut di dalam **Routes.php**:

```php
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```

Untuk mengetahui route yang ditambahkan sudah benar, buka CLI dan jalankan:

```
php spark routes
```

> 📸 **[Screenshot: Tampilan daftar route di CLI setelah menjalankan php spark routes]**

Ketika route diakses tanpa Controller yang sesuai, akan muncul error 404.

> 📸 **[Screenshot: Tampilan error 404 File Not Found]**

---

### 8. Membuat Controller
Buat file baru dengan nama **Page.php** pada direktori **app/Controllers/**:

```php
<?php

namespace App\Controllers;

class Page extends BaseController
{
    public function about()
    {
        return view('about', [
            'title'   => 'Halaman About',
            'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
        ]);
    }

    public function contact()
    {
        return view('contact', [
            'title'   => 'Halaman Contact',
            'content' => 'Ini adalah halaman contact. Silakan hubungi kami.'
        ]);
    }

    public function faqs()
    {
        return view('faqs', [
            'title'   => 'Halaman FAQ',
            'content' => 'Ini adalah halaman FAQ berisi pertanyaan yang sering ditanyakan.'
        ]);
    }
}
```

> 📸 **[Screenshot: Tampilan halaman About setelah Controller berhasil dibuat]**

---

### 9. Membuat View
Buat file baru dengan nama **about.php** pada direktori **app/Views/**:

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
</head>
<body>
    <h1><?= $title; ?></h1>
    <hr>
    <p><?= $content; ?></p>
</body>
</html>
```

> 📸 **[Screenshot: Tampilan halaman About dengan judul dan konten]**

---

### 10. Membuat Layout Web dengan CSS
Pada Codeigniter 4, file yang menyimpan asset CSS dan JavaScript terletak pada direktori **public**.

Buat file **style.css** pada direktori **public/**.

Kemudian buat folder **template** pada direktori **app/Views/** dan buat file **header.php** dan **footer.php**.

#### File app/Views/template/header.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
```

#### File app/Views/template/footer.php
```php
            </section>
            <aside id="sidebar">
                <div class="widget-box">
                    <h3 class="title">Widget Header</h3>
                    <ul>
                        <li><a href="#">Widget Link</a></li>
                        <li><a href="#">Widget Link</a></li>
                    </ul>
                </div>
                <div class="widget-box">
                    <h3 class="title">Widget Text</h3>
                    <p>Vestibulum lorem elit, iaculis in nisl volutpat, malesuada tincidunt arcu.</p>
                </div>
            </aside>
        </section>
        <footer>
            <p>&copy; 2021 - Universitas Pelita Bangsa</p>
        </footer>
    </div>
</body>
</html>
```

Kemudian ubah file **app/Views/about.php** menjadi:

```php
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```

> 📸 **[Screenshot: Tampilan halaman About dengan layout lengkap (header, nav, sidebar, footer)]**

---

## Pertanyaan dan Tugas
Lengkapi kode program untuk menu lainnya yang ada pada Controller Page, sehingga semua link pada navigasi header dapat menampilkan tampilan dengan layout yang sama.

**Jawaban:**
Membuat view untuk halaman **contact.php** dan **faqs.php** dengan menggunakan template header dan footer yang sama, serta mengupdate method `contact()` dan `faqs()` pada Controller Page untuk memanggil view yang sesuai.

> 📸 **[Screenshot: Tampilan halaman Contact dengan layout yang sama]**

> 📸 **[Screenshot: Tampilan halaman FAQ dengan layout yang sama]**

---

## Hasil Akhir
Tampilan akhir website dengan layout lengkap:
- ✅ Header dengan judul "Layout Sederhana"
- ✅ Navigasi menu (Home, Artikel, About, Kontak)
- ✅ Konten utama di bagian kiri
- ✅ Sidebar dengan Widget Header dan Widget Text di bagian kanan
- ✅ Footer di bagian bawah
<img width="1919" height="924" alt="Cuplikan layar 2026-03-29 221700" src="https://github.com/user-attachments/assets/9809f4d1-24c0-4b6a-9b97-4a16846c9647" />

<img width="963" height="301" alt="Cuplikan layar 2026-03-29 222216" src="https://github.com/user-attachments/assets/d484761a-4ff4-4b09-b129-bdbeead4b4ee" />

<img width="954" height="997" alt="Cuplikan layar 2026-03-29 222247" src="https://github.com/user-attachments/assets/524e8d54-2012-49ea-afdc-1cfdc5a68e97" />

<img width="1919" height="704" alt="image" src="https://github.com/user-attachments/assets/6942d15e-c076-4983-bfd0-9cf7e54e4e86" />

setelah ditambahkan satu artikel
<img width="963" height="661" alt="image" src="https://github.com/user-attachments/assets/36b9fea3-b001-4636-aa56-b343d7544ddf" />

<img width="910" height="360" alt="image" src="https://github.com/user-attachments/assets/fb6e6e4f-6abb-4450-a26e-11ea3770cd8f" />

<img width="1243" height="553" alt="image" src="https://github.com/user-attachments/assets/a9caec2e-482a-4823-a5b6-4e81612a0b17" />

<img width="1567" height="679" alt="image" src="https://github.com/user-attachments/assets/0d6390c5-8b5f-4b1b-9bd3-77811836f018" />

<img width="1919" height="767" alt="image" src="https://github.com/user-attachments/assets/0383af2a-31d0-4bfb-87d8-a070c52c253c" />



# PRAKTIKUM 2

<img width="1918" height="766" alt="image" src="https://github.com/user-attachments/assets/1329ee4b-d91a-41c2-bcf5-db88395b1f09" />

<img width="1919" height="746" alt="image" src="https://github.com/user-attachments/assets/9bd4b193-e751-443a-a0e1-26d3885e5d4f" />

<img width="1919" height="730" alt="image" src="https://github.com/user-attachments/assets/fafba2f1-0bc7-4e95-b2df-683c5ccc0e7b" />

<img width="962" height="614" alt="image" src="https://github.com/user-attachments/assets/240a200f-b9ab-47cf-b57f-5b0929be518b" />

<img width="1919" height="727" alt="image" src="https://github.com/user-attachments/assets/59bff7be-eedd-4998-8820-8758701eea65" />

setelah ditambahkan satu artikel
<img width="963" height="661" alt="image" src="https://github.com/user-attachments/assets/36b9fea3-b001-4636-aa56-b343d7544ddf" />

setelah salah satu artikrlnya di hapus

<img width="1907" height="625" alt="image" src="https://github.com/user-attachments/assets/d600d0d0-3667-4717-82ef-926559a56179" />

# PRAKTIKUM 3

<img width="1714" height="761" alt="image" src="https://github.com/user-attachments/assets/4a7f7bce-62e6-4672-8898-b18739f43877" />

Pertanyaan 1:

Apa manfaat utama dari penggunaan View Layout dalam pengembangan aplikasi?

Jawaban:
View Layout memungkinkan kita membuat template tampilan yang konsisten di semua halaman. Cukup ubah satu file layout, semua halaman yang menggunakannya akan ikut berubah. Ini membuat kode lebih efisien, terstruktur, dan mudah dipelihara.

Pertanyaan 2:

Jelaskan perbedaan antara View Cell dan View biasa.

Jawaban:
View biasa dipanggil langsung dari Controller dan menampilkan seluruh halaman. Sedangkan View Cell adalah komponen kecil yang bisa dipanggil dari dalam View manapun secara mandiri, memiliki logika sendiri untuk mengambil data, dan dapat digunakan ulang di berbagai halaman tanpa harus melewati Controller.
