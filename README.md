 # Lab7Web-Semester4

**Nama : Alipiani Dwi Putri**
**NIM : 312410691**
**Kelas : TI24 A.2**
**Mata Kuliah : Pemrograman Web2**
Dosen : Agung Nugroho, S.Kom., M.Kom.

---


# Praktikum 1: PHP Framework (Codeigniter)

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

<img width="976" height="625" alt="image" src="https://github.com/user-attachments/assets/2dc4ac2b-0957-4ce0-9402-3c7f1fb2442d" />

---

### 2. Instalasi Codeigniter 4
Untuk melakukan instalasi Codeigniter 4 dapat dilakukan dengan dua cara, yaitu cara manual dan menggunakan composer. Pada praktikum ini kita menggunakan cara manual.

- Unduh **Codeigniter** dari website https://codeigniter.com/download
- Extrak file zip Codeigniter ke direktori **htdocs/lab11_ci**
- Ubah nama direktori **framework-4.x.xx** menjadi **ci4**
- Buka browser dengan alamat http://localhost/lab11_ci/ci4/public/

<img width="1919" height="924" alt="Cuplikan layar 2026-03-29 221700" src="https://github.com/user-attachments/assets/9809f4d1-24c0-4b6a-9b97-4a16846c9647" />

---

### 3. Menjalankan CLI (Command Line Interface)
Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk mengakses CLI buka terminal/command prompt.

Arahkan lokasi direktori sesuai dengan direktori kerja project dibuat **(xampp/htdocs/lab11_ci/ci4/)**

Perintah yang dapat dijalankan untuk memanggil CLI Codeigniter adalah:

```
php spark
```

<img width="954" height="997" alt="Cuplikan layar 2026-03-29 222247" src="https://github.com/user-attachments/assets/524e8d54-2012-49ea-afdc-1cfdc5a68e97" />

---

### 4. Mengaktifkan Mode Debugging
Codeigniter 4 menyediakan fitur **debugging** untuk memudahkan developer untuk mengetahui pesan error apabila terjadi kesalahan dalam membuat kode program.

Secara default fitur ini belum aktif. Ketika terjadi error pada aplikasi akan ditampilkan pesan kesalahan **"Whoops!"** yang tidak informatif.

<img width="1919" height="704" alt="image" src="https://github.com/user-attachments/assets/6942d15e-c076-4983-bfd0-9cf7e54e4e86" />
Untuk mengaktifkan mode debugging:
- Ubah nama file **env** menjadi **.env**
- Buka file tersebut dan ubah nilai variable **CI_ENVIRONMENT** menjadi **development**

```
CI_ENVIRONMENT = development
```

<img width="532" height="178" alt="image" src="https://github.com/user-attachments/assets/b5b360e3-8d90-4c71-a1a3-0a1b6777e75b" />

Setelah mode debugging aktif, pesan error akan ditampilkan lebih detail seperti **ParseError** beserta nama file dan nomor baris yang menyebabkan error.

<img width="488" height="311" alt="image" src="https://github.com/user-attachments/assets/ca63867d-4ea5-42de-beb1-cc227b67f3c8" />


---

### 5. Struktur Direktori
Untuk lebih memahami Framework Codeigniter 4 perlu mengetahui struktur direktori dan file yang ada. Buka pada **Windows Explorer** atau dari **Visual Studio Code -> Open Folder**.

<img width="1439" height="847" alt="image" src="https://github.com/user-attachments/assets/39544d74-fa6f-4340-aa46-7b34a272a4e4" />


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

<img width="1713" height="409" alt="image" src="https://github.com/user-attachments/assets/4463e363-920a-4346-826a-f5772d3f1f93" />


Ketika route diakses tanpa Controller yang sesuai, akan muncul error 404.

<img width="593" height="367" alt="image" src="https://github.com/user-attachments/assets/c05505ea-5c3d-418f-ad1f-a8fcaf686a9b" />

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

<img width="910" height="360" alt="image" src="https://github.com/user-attachments/assets/fb6e6e4f-6abb-4450-a26e-11ea3770cd8f" />

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

<img width="963" height="661" alt="image" src="https://github.com/user-attachments/assets/36b9fea3-b001-4636-aa56-b343d7544ddf" />

<img width="1919" height="767" alt="image" src="https://github.com/user-attachments/assets/0383af2a-31d0-4bfb-87d8-a070c52c253c" />


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
- Header dengan judul "Layout Sederhana"
- Navigasi menu (Home, Artikel, About, Kontak)
- Konten utama di bagian kiri
- Sidebar dengan Widget Header dan Widget Text di bagian kanan 
- Footer di bagian bawah


# PRAKTIKUM 2: Framework Lanjutan (CRUD)

---

## Langkah-langkah Praktikum

### 1. Persiapan Database
Untuk memulai membuat aplikasi CRUD sederhana, yang perlu disiapkan adalah database server menggunakan MySQL. Pastikan MySQL Server sudah dapat dijalankan melalui XAMPP.

#### Membuat Database
```sql
CREATE DATABASE lab_ci4;
```

#### Membuat Tabel Artikel
```sql
CREATE TABLE artikel (
    id INT(11) auto_increment,
    judul VARCHAR(200) NOT NULL,
    isi TEXT,
    gambar VARCHAR(200),
    status TINYINT(1) DEFAULT 0,
    slug VARCHAR(200),
    PRIMARY KEY(id)
);
```

---

### 2. Konfigurasi Koneksi Database
Selanjutnya membuat konfigurasi untuk menghubungkan dengan database server. Konfigurasi dilakukan pada file **.env** dengan menghapus tanda `#` dan mengisi nilai berikut:

```
database.default.hostname = localhost
database.default.database = lab_ci4
database.default.username = root
database.default.password = 
database.default.DBDriver = MySQLi
database.default.DBPrefix =
```

<img width="888" height="302" alt="image" src="https://github.com/user-attachments/assets/04d326da-a040-46d7-b8db-559b484dd34f" />

---

### 3. Membuat Model
Selanjutnya adalah membuat Model untuk memproses data Artikel. Buat file baru pada direktori **app/Models** dengan nama **ArtikelModel.php**:

```php
<?php

namespace App\Models;

use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
}
```

---

### 4. Membuat Controller Artikel
Buat Controller baru dengan nama **Artikel.php** pada direktori **app/Controllers**:

```php
<?php

namespace App\Controllers;

use App\Models\ArtikelModel;

class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/index', compact('artikel', 'title'));
    }

    public function view($slug)
    {
        $model = new ArtikelModel();
        $artikel = $model->where(['slug' => $slug])->first();

        if (!$artikel)
        {
            throw \CodeIgniter\Exceptions\PageNotFoundException::forPageNotFound();
        }

        $title = $artikel['judul'];
        return view('artikel/detail', compact('artikel', 'title'));
    }

    public function admin_index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/admin_index', compact('artikel', 'title'));
    }

    public function add()
    {
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();

        if ($isDataValid)
        {
            $artikel = new ArtikelModel();
            $artikel->insert([
                'judul' => $this->request->getPost('judul'),
                'isi'   => $this->request->getPost('isi'),
                'slug'  => url_title($this->request->getPost('judul')),
            ]);
            return redirect()->to('/admin/artikel');
        }

        $title = "Tambah Artikel";
        return view('artikel/form_add', compact('title'));
    }

    public function edit($id)
    {
        $artikel = new ArtikelModel();

        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();

        if ($isDataValid)
        {
            $artikel->update($id, [
                'judul' => $this->request->getPost('judul'),
                'isi'   => $this->request->getPost('isi'),
            ]);
            return redirect()->to('/admin/artikel');
        }

        $data = $artikel->where('id', $id)->first();
        $title = "Edit Artikel";
        return view('artikel/form_edit', compact('title', 'data'));
    }

    public function delete($id)
    {
        $artikel = new ArtikelModel();
        $artikel->delete($id);
        return redirect()->to('/admin/artikel');
    }
}
```

---

### 5. Membuat View Index Artikel
Buat direktori baru dengan nama **artikel** pada direktori **app/Views**, kemudian buat file baru dengan nama **index.php**:

```php
<?= $this->include('template/header'); ?>

<?php if($artikel): foreach($artikel as $row): ?>
<article class="entry">
    <h2><a href="<?= base_url('/artikel/' . $row['slug']);?>"><?= $row['judul']; ?></a></h2>
    <img src="<?= base_url('/gambar/' . $row['gambar']);?>" alt="<?= $row['judul']; ?>">
    <p><?= substr($row['isi'], 0, 200); ?></p>
</article>
<hr class="divider" />
<?php endforeach; else: ?>
<article class="entry">
    <h2>Belum ada data.</h2>
</article>
<?php endif; ?>

<?= $this->include('template/footer'); ?>
```

Selanjutnya buka browser dengan mengakses url `http://localhost/lab11_ci/ci4/public/artikel`

<img width="1918" height="766" alt="image" src="https://github.com/user-attachments/assets/1329ee4b-d91a-41c2-bcf5-db88395b1f09" />

---

### 6. Menambahkan Data Artikel
Tambahkan beberapa data pada database agar dapat ditampilkan datanya dengan menjalankan query berikut di phpMyAdmin:

```sql
INSERT INTO artikel (judul, isi, slug) VALUES
('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy dalam industri percetakan dan penataan huruf atau typesetting. Lorem Ipsum telah menjadi standar contoh teks sejak tahun 1500an, saat seorang tukang cetak yang tidak dikenal mengambil sebuah kumpulan teks dan mengacaknya untuk menjadi sebuah buku contoh huruf.', 'artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang, Lorem Ipsum bukanlah teks-teks yang diacak. Ia berakar dari sebuah naskah sastra latin klasik dari era 45 sebelum masehi, hingga bisa dipastikan usianya telah mencapai lebih dari 2000 tahun.', 'artikel-kedua');
```

Refresh kembali browser, sehingga akan ditampilkan hasilnya.

<img width="1919" height="746" alt="image" src="https://github.com/user-attachments/assets/9bd4b193-e751-443a-a0e1-26d3885e5d4f" />

---

### 7. Membuat Tampilan Detail Artikel
Tambahkan fungsi baru pada Controller Artikel dengan nama **view()** (sudah ada di Controller di atas).

Buat view baru untuk halaman detail dengan nama **app/Views/artikel/detail.php**:

```php
<?= $this->include('template/header'); ?>

<article class="entry">
    <h2><?= $artikel['judul']; ?></h2>
    <img src="<?= base_url('/gambar/' . $artikel['gambar']);?>" alt="<?= $artikel['judul']; ?>">
    <p><?= $artikel['isi']; ?></p>
</article>

<?= $this->include('template/footer'); ?>
```

Tambahkan routing untuk artikel detail di **app/Config/Routes.php**:

```php
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
```

<img width="1919" height="730" alt="image" src="https://github.com/user-attachments/assets/fafba2f1-0bc7-4e95-b2df-683c5ccc0e7b" />

---

### 8. Membuat Menu Admin
Menu admin adalah untuk proses CRUD data artikel. Tambahkan method **admin_index()** pada Controller Artikel (sudah ada di Controller di atas).

Buat file **admin_index.php** pada direktori **app/Views/artikel/**:

```php
<?= $this->include('template/admin_header'); ?>

<table class="table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </thead>
    <tbody>
        <?php if($artikel): foreach($artikel as $row): ?>
        <tr>
            <td><?= $row['id']; ?></td>
            <td>
                <b><?= $row['judul']; ?></b>
                <p><small><?= substr($row['isi'], 0, 50); ?></small></p>
            </td>
            <td><?= $row['status']; ?></td>
            <td>
                <a class="btn" href="<?= base_url('/admin/artikel/edit/' . $row['id']);?>">Ubah</a>
                <a class="btn btn-danger" onclick="return confirm('Yakin menghapus data?');" href="<?= base_url('/admin/artikel/delete/' . $row['id']);?>">Hapus</a>
            </td>
        </tr>
        <?php endforeach; else: ?>
        <tr>
            <td colspan="4">Belum ada data.</td>
        </tr>
        <?php endif; ?>
    </tbody>
    <tfoot>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </tfoot>
</table>

<?= $this->include('template/admin_footer'); ?>
```

Tambahkan routing untuk menu admin di **app/Config/Routes.php**:

```php
$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```

Akses menu admin dengan url `http://localhost/lab11_ci/ci4/public/admin/artikel`

<img width="962" height="614" alt="image" src="https://github.com/user-attachments/assets/240a200f-b9ab-47cf-b57f-5b0929be518b" />

---

### 9. Menambah Data Artikel (Form Add)
Buat view untuk form tambah dengan nama **form_add.php** pada direktori **app/Views/artikel/**:

```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <label>Judul</label><br>
        <input type="text" name="judul" style="width:100%; padding:8px;">
    </p>
    <p>
        <label>Isi Artikel</label><br>
        <textarea name="isi" cols="50" rows="10" style="width:100%; padding:8px;"></textarea>
    </p>
    <p>
        <input type="submit" value="Kirim" class="btn btn-large">
    </p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

<img width="1919" height="727" alt="image" src="https://github.com/user-attachments/assets/59bff7be-eedd-4998-8820-8758701eea65" />
---

### 10. Mengubah Data Artikel (Form Edit)
Buat view untuk form edit dengan nama **form_edit.php** pada direktori **app/Views/artikel/**:

```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <label>Judul</label><br>
        <input type="text" name="judul" value="<?= $data['judul'];?>" style="width:100%; padding:8px;">
    </p>
    <p>
        <label>Isi Artikel</label><br>
        <textarea name="isi" cols="50" rows="10" style="width:100%; padding:8px;"><?= $data['isi'];?></textarea>
    </p>
    <p>
        <input type="submit" value="Kirim" class="btn btn-large">
    </p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

<img width="1914" height="829" alt="image" src="https://github.com/user-attachments/assets/b08031b8-2874-4133-a531-c6630fd9b2a7" />

---

Setelah menambah satu artikel

<img width="963" height="661" alt="image" src="https://github.com/user-attachments/assets/36b9fea3-b001-4636-aa56-b343d7544ddf" />

---

### 11. Menghapus Data Artikel
Fungsi hapus data sudah ada pada method **delete()** di Controller Artikel. Ketika tombol **Hapus** diklik, akan muncul konfirmasi "Yakin menghapus data?" sebelum data dihapus dari database.

Salah satu Data Yang sudah dihapus
<img width="1907" height="625" alt="image" src="https://github.com/user-attachments/assets/d600d0d0-3667-4717-82ef-926559a56179" />

---

## Hasil Akhir Praktikum 2

Fitur CRUD yang berhasil dibuat:
- **Read** - Menampilkan daftar artikel di halaman publik
- **Read Detail** - Menampilkan detail artikel saat judul diklik
- **Create** - Form tambah artikel baru di halaman admin
- **Update** - Form edit artikel yang sudah ada
- **Delete** - Hapus artikel dengan konfirmasi


<img width="1919" height="730" alt="image" src="https://github.com/user-attachments/assets/fafba2f1-0bc7-4e95-b2df-683c5ccc0e7b" />

<img width="962" height="614" alt="image" src="https://github.com/user-attachments/assets/240a200f-b9ab-47cf-b57f-5b0929be518b" />

<img width="1919" height="727" alt="image" src="https://github.com/user-attachments/assets/59bff7be-eedd-4998-8820-8758701eea65" />



# PRAKTIKUM 3: View Layout dan View Cell

## Langkah-langkah Praktikum

### 1. Persiapan
Pada praktikum sebelumnya kita telah menggunakan template layout dengan konsep parsial atau memecah bagian template menjadi beberapa bagian untuk kemudian di include pada view yang lain.

Praktikum kali ini kita akan menggunakan konsep **View Layout** dan **View Cell** untuk memudahkan dalam penggunaan layout.

Tambahkan field **created_at** pada tabel artikel di database:

```sql
ALTER TABLE artikel ADD COLUMN created_at DATETIME DEFAULT CURRENT_TIMESTAMP;
```

---

### 2. Membuat Layout Utama
Buat folder **layout** di dalam **app/Views/**, kemudian buat file **main.php** di dalam folder layout:

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title ?? 'My Website' ?></title>
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
                <?= $this->renderSection('content') ?>
            </section>
            <aside id="sidebar">
                <?= view_cell('App\\Cells\\ArtikelTerkini::render') ?>
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

---

### 3. Modifikasi File View
Ubah file **app/Views/about.php** agar sesuai dengan layout baru:

```php
<?= $this->extend('layout/main') ?>

<?= $this->section('content') ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->endSection() ?>
```

Lakukan hal yang sama untuk file **contact.php**, **faqs.php**, dan **artikel/index.php**.

---

### 4. Membuat Class View Cell
View Cell adalah fitur yang memungkinkan pemanggilan tampilan dalam bentuk komponen yang dapat digunakan ulang.

Buat folder **Cells** di dalam **app/**, kemudian buat file **ArtikelTerkini.php**:

```php
<?php

namespace App\Cells;

use App\Models\ArtikelModel;

class ArtikelTerkini
{
    public function render()
    {
        $model = new ArtikelModel();
        $artikel = $model->orderBy('created_at', 'DESC')->limit(5)->findAll();
        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```

---

### 5. Membuat View untuk View Cell
Buat folder **components** di dalam **app/Views/**, kemudian buat file **artikel_terkini.php**:

```php
<div class="widget-box">
    <h3 class="title">Artikel Terkini</h3>
    <ul>
        <?php foreach ($artikel as $row): ?>
        <li><a href="<?= base_url('/artikel/' . $row['slug']) ?>"><?= $row['judul'] ?></a></li>
        <?php endforeach; ?>
    </ul>
</div>
```

---

### 6. Hasil Akhir
Refresh browser dan akses halaman:
```
localhost/lab11_ci/ci4/public/about
```

<img width="1714" height="761" alt="image" src="https://github.com/user-attachments/assets/4a7f7bce-62e6-4672-8898-b18739f43877" />
---

## Pertanyaan dan Tugas

**1. Apa manfaat utama dari penggunaan View Layout dalam pengembangan aplikasi?**

View Layout memungkinkan kita membuat template tampilan yang konsisten di semua halaman. Cukup ubah satu file layout, semua halaman yang menggunakannya akan ikut berubah. Ini membuat kode lebih efisien, terstruktur, dan mudah dipelihara.

**2. Jelaskan perbedaan antara View Cell dan View biasa.**

View biasa dipanggil langsung dari Controller dan menampilkan seluruh halaman. Sedangkan View Cell adalah komponen kecil yang bisa dipanggil dari dalam View manapun secara mandiri, memiliki logika sendiri untuk mengambil data, dan dapat digunakan ulang di berbagai halaman tanpa harus melewati Controller.

---

# Praktikum 4

<img width="1919" height="649" alt="image" src="https://github.com/user-attachments/assets/1654c1cb-928e-465b-9d14-963fb3cd31b6" />


