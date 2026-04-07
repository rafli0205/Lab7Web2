# Praktikum CodeIgniter 4 - Modul 1 sampai 4

**Nama** : Rafli Dhiya Fadhaly\
**NIM** : 312410251\
**Kelas** : I241B\
**Dosen** : Agung Nugroho, S.Kom., M.Kom.\
**Mata Kuliah** : Pemrograman Web 2

## Identitas Project
Project ini merupakan hasil praktikum pembuatan website menggunakan framework **CodeIgniter 4**.  
Pengembangan project dilakukan secara bertahap dari **Praktikum 1 sampai Praktikum 4** dengan fokus pada pemahaman dasar framework, routing, controller, model, view, CRUD artikel, login, session, dan filter auth.

Project ini dibuat untuk memahami bagaimana membangun website dinamis berbasis MVC menggunakan CodeIgniter 4.  
Website memiliki halaman publik dan halaman admin untuk pengelolaan artikel. [file:111][file:113][file:34]

---

# Daftar Isi
- Deskripsi Project
- Tujuan Praktikum
- Tools dan Teknologi
- Struktur Fitur Project
- Penjelasan Praktikum 1
- Penjelasan Praktikum 2
- Penjelasan Praktikum 3
- Penjelasan Praktikum 4
- Struktur Routing
- Struktur Controller
- Struktur Database
- Alur Sistem
- Potongan Kode Penting
- Hasil yang Dicapai
- Kendala Project
- Kesimpulan
- Developer

---

# Deskripsi Project
Website ini merupakan aplikasi web sederhana berbasis CodeIgniter 4 yang memiliki dua bagian utama:

1. **Halaman publik**, yang dapat diakses oleh semua pengunjung.
2. **Halaman admin**, yang digunakan untuk mengelola artikel setelah berhasil login.

Fitur publik meliputi halaman Home, About, Contact, FAQ, daftar artikel, dan detail artikel.  
Fitur admin meliputi login, logout, daftar artikel admin, tambah artikel, edit artikel, dan hapus artikel. [file:111][file:113][file:34]

---

# Tujuan Praktikum
Tujuan dari praktikum ini adalah:

- Memahami dasar penggunaan framework CodeIgniter 4.
- Memahami konsep MVC (Model, View, Controller).
- Membuat routing halaman statis dan dinamis.
- Menghubungkan aplikasi dengan database.
- Menampilkan data artikel dari database.
- Membuat fitur CRUD artikel.
- Membuat sistem login admin.
- Menggunakan session untuk autentikasi.
- Menggunakan filter auth untuk membatasi akses halaman admin.

---

# Tools dan Teknologi
Project ini dibangun menggunakan:

- **PHP**
- **CodeIgniter 4**
- **MySQL**
- **phpMyAdmin**
- **HTML**
- **CSS**

Database digunakan untuk menyimpan data artikel dan data user/admin, sedangkan CodeIgniter 4 digunakan sebagai framework utama dengan pola MVC. [file:113][file:34]

---

# Struktur Fitur Project

## Fitur Halaman Publik
- Home
- About
- Contact
- FAQ
- Daftar artikel
- Detail artikel

## Fitur User/Admin
- Login
- Logout
- Daftar user

## Fitur Admin Artikel
- Daftar artikel admin
- Tambah artikel
- Edit artikel
- Hapus artikel

Semua fitur tersebut terlihat dari struktur route dan controller pada source code project. [file:111][file:113][file:34]

---

# Praktikum 1 - Pengenalan CodeIgniter 4

## Penjelasan
Pada praktikum pertama, dilakukan pengenalan dasar framework CodeIgniter 4.  
Tahap ini merupakan fondasi awal sebelum masuk ke pembuatan halaman, model, dan database.

Praktikum 1 umumnya berisi:
- instalasi CodeIgniter 4,
- menjalankan project di browser,
- memahami struktur folder project,
- memahami file konfigurasi dasar.

## Materi yang Dipelajari
- Instalasi CodeIgniter 4
- Menjalankan server lokal
- Struktur folder CI4
- Pengenalan controller
- Tampilan halaman awal

## Struktur Folder Penting
Beberapa folder penting pada CodeIgniter 4:
- `app/Controllers`
- `app/Models`
- `app/Views`
- `app/Config`
- `public`
- `writable`

## Hasil Praktikum 1
Pada tahap ini, project sudah bisa dijalankan di localhost dan menampilkan halaman awal framework.  
Praktikum 1 menjadi dasar untuk melanjutkan ke routing, controller, dan halaman dinamis pada modul selanjutnya.

---

# Praktikum 2 - Routing, Controller, dan View

## Penjelasan
Pada praktikum 2, aplikasi mulai dikembangkan dengan membuat beberapa halaman website statis.  
Materi utamanya berfokus pada **routing**, **controller**, dan **view**.

## Materi yang Dipelajari
- Membuat route di `Routes.php`
- Membuat controller
- Membuat method pada controller
- Membuat file view
- Menampilkan halaman berdasarkan route

## Implementasi pada Project
Pada project ini, route publik yang dibuat antara lain:

- `/`
- `/about`
- `/contact`
- `/faqs` [file:111]

Route tersebut diarahkan ke controller yang sesuai, misalnya:
- `Home::index`
- `Page::about`
- `Page::contact`
- `Page::faqs` [file:111]

## Contoh Kode Routing
```php
$routes->get('/', 'Home::index');
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```
[file:111]

## Hasil Praktikum 2
Pada tahap ini website sudah memiliki halaman publik statis yang dapat diakses melalui browser sesuai route masing-masing. [file:111]

---

# Praktikum 3 - Model, Database, dan Artikel

## Penjelasan
Pada praktikum 3, website mulai dikembangkan menjadi aplikasi dinamis dengan menggunakan database.  
Data yang dikelola pada project ini adalah **artikel**.

## Materi yang Dipelajari
- Membuat database
- Membuat tabel artikel
- Membuat model artikel
- Mengambil data dari database
- Menampilkan daftar artikel
- Menampilkan detail artikel berdasarkan slug
- Membuat CRUD artikel

## Implementasi pada Project
Pada source code project, controller `Artikel` memiliki beberapa method penting:

- `index()` → menampilkan daftar artikel
- `view($slug)` → menampilkan detail artikel
- `admin_index()` → menampilkan artikel pada halaman admin
- `add()` → menambah artikel
- `edit($id)` → mengedit artikel
- `delete($id)` → menghapus artikel [file:113]

## Contoh Kode Controller Artikel
```php
public function index()
{
    $title = 'Daftar Artikel';
    $model = new ArtikelModel();
    $artikel = $model->findAll();

    return view('artikel/index', compact('artikel', 'title'));
}
```
[file:113]

## Detail Artikel Berdasarkan Slug
```php
public function view($slug)
{
    $model = new ArtikelModel();
    $artikel = $model->where(['slug' => $slug])->first();

    if (! $artikel) {
        throw PageNotFoundException::forPageNotFound();
    }

    $title = $artikel['judul'];
    return view('artikel/detail', compact('artikel', 'title'));
}
```
[file:113]

## CRUD Artikel Admin
### Tambah Artikel
```php
public function add()
{
    $validation = \Config\Services::validation();
    $validation->setRules(['judul' => 'required']);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid) {
        $artikel = new ArtikelModel();
        $artikel->insert([
            'judul' => $this->request->getPost('judul'),
            'isi' => $this->request->getPost('isi'),
            'slug' => url_title($this->request->getPost('judul')),
        ]);

        return redirect('admin/artikel');
    }

    $title = 'Tambah Artikel';
    return view('artikel/form_add', compact('title'));
}
```
[file:113]

### Edit Artikel
```php
public function edit($id)
{
    $artikel = new ArtikelModel();

    $validation = \Config\Services::validation();
    $validation->setRules(['judul' => 'required']);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid) {
        $artikel->update($id, [
            'judul' => $this->request->getPost('judul'),
            'isi' => $this->request->getPost('isi'),
        ]);

        return redirect('admin/artikel');
    }

    $data = $artikel->where('id', $id)->first();
    $title = 'Edit Artikel';
    return view('artikel/form_edit', compact('title', 'data'));
}
```
[file:113]

### Hapus Artikel
```php
public function delete($id)
{
    $artikel = new ArtikelModel();
    $artikel->delete($id);

    return redirect('admin/artikel');
}
```
[file:113]

## Hasil Praktikum 3
Pada tahap ini, website sudah dapat:
- Menampilkan daftar artikel dari database
- Menampilkan detail artikel berdasarkan slug
- Mengelola artikel dari sisi admin [file:113]

---

# Praktikum 4 - Login, Session, dan Filter Auth

## Penjelasan
Pada praktikum 4, aplikasi dikembangkan dengan sistem login admin.  
Login digunakan agar hanya user tertentu yang dapat mengakses halaman admin dan melakukan pengelolaan artikel.

## Materi yang Dipelajari
- Membuat form login
- Mengambil input email dan password
- Menghubungkan login dengan tabel user
- Menggunakan `password_verify()`
- Menyimpan session login
- Membuat logout
- Membatasi akses admin menggunakan filter auth

## Route Login dan Admin
Pada source code project, route login dan admin ditulis sebagai berikut:

```php
$routes->match(['get', 'post'], 'user/login', 'User::login');
$routes->get('user', 'User::index');
$routes->get('user/logout', 'User::logout');

$routes->group('admin', ['filter' => 'auth'], function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->match(['get', 'post'], 'artikel/add', 'Artikel::add');
    $routes->match(['get', 'post'], 'artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```
[file:111]

Route tersebut menunjukkan bahwa:
- login dapat diakses melalui `user/login`,
- logout melalui `user/logout`,
- dan seluruh route admin dilindungi filter `auth`. [file:111]

## Controller Login
Pada controller `User`, proses login dilakukan dengan:
1. mengambil input email,
2. mengambil input password,
3. mencari user berdasarkan `useremail`,
4. memverifikasi password dengan `password_verify()`,
5. menyimpan session login,
6. redirect ke halaman admin artikel. [file:34]

## Contoh Kode Login
```php
public function login()
{
    helper(['form']);
    $email = $this->request->getPost('email');
    $password = $this->request->getPost('password');

    if (!$email) {
        return view('user/login');
    }

    $session = session();
    $model = new UserModel();
    $login = $model->where('useremail', $email)->first();

    if ($login) {
        $pass = $login['userpassword'];
        if (password_verify($password, $pass)) {
            $login_data = [
                'user_id' => $login['id'],
                'user_name' => $login['username'],
                'user_email' => $login['useremail'],
                'logged_in' => TRUE,
            ];
            $session->set($login_data);
            return redirect('admin/artikel');
        } else {
            $session->setFlashdata("flash_msg", "Password salah.");
            return redirect()->to('/user/login');
        }
    } else {
        $session->setFlashdata("flash_msg", "email tidak terdaftar.");
        return redirect()->to('/user/login');
    }
}
```
[file:34]

## Logout
```php
public function logout()
{
    session()->destroy();
    return redirect()->to('/user/login');
}
```
[file:34]

## Mekanisme Login
Alur login pada project ini adalah:
- user membuka halaman login,
- user memasukkan email dan password,
- sistem mencari email pada tabel user,
- sistem membandingkan password input dengan hash di database,
- jika benar maka session `logged_in` disimpan,
- user diarahkan ke `/admin/artikel`. [file:34]

## Filter Auth
Route admin menggunakan filter `auth` agar tidak dapat diakses tanpa login. [file:111]

## Hasil Praktikum 4
Pada tahap ini project sudah memiliki:
- form login,
- proses autentikasi dasar,
- session login,
- logout,
- pembatasan route admin dengan auth filter. [file:34][file:111]

## Catatan Pengembangan
Pada tahap implementasi, proses login masih mengalami kendala pada pengujian tertentu, terutama pada bagian redirect dan session setelah login. Namun struktur login, session, dan route auth sudah berhasil dibuat sesuai alur praktikum. [file:34][file:111]

---

# Struktur Routing

## Halaman Publik
- `/` → Home
- `/about` → About
- `/contact` → Contact
- `/faqs` → FAQ
- `/artikel` → Daftar artikel
- `/artikel/(:any)` → Detail artikel [file:111]

## Halaman User
- `/user/login` → Login
- `/user` → Daftar user
- `/user/logout` → Logout [file:111]

## Halaman Admin
- `/admin/artikel` → Daftar artikel admin
- `/admin/artikel/add` → Tambah artikel
- `/admin/artikel/edit/{id}` → Edit artikel
- `/admin/artikel/delete/{id}` → Hapus artikel [file:111]

---

# Struktur Controller

## Controller Artikel
Controller `Artikel` digunakan untuk:
- mengambil data artikel,
- menampilkan daftar artikel,
- menampilkan detail artikel,
- menambah artikel,
- mengubah artikel,
- menghapus artikel. [file:113]

## Controller User
Controller `User` digunakan untuk:
- menampilkan daftar user,
- menangani login,
- menangani logout,
- menyimpan session login. [file:34]

---

# Struktur Database

## Tabel User
Field yang digunakan pada project:
- `id`
- `username`
- `useremail`
- `userpassword` [file:34]

Password pada kolom `userpassword` disimpan dalam bentuk hash dan diverifikasi menggunakan `password_verify()`. [file:34]

## Tabel Artikel
Tabel artikel digunakan untuk menyimpan:
- judul artikel
- isi artikel
- slug artikel

Slug dipakai untuk menampilkan detail artikel berdasarkan URL. [file:113]

---

# Alur Sistem

## Alur Pengunjung
1. Pengunjung membuka halaman Home, About, Contact, FAQ, atau Artikel. [file:111]
2. Pengunjung dapat melihat daftar artikel. [file:113]
3. Pengunjung dapat membuka detail artikel menggunakan slug. [file:111][file:113]

## Alur Admin
1. Admin membuka halaman `/user/login`. [file:111]
2. Admin memasukkan email dan password. [file:34]
3. Sistem memvalidasi email dan password. [file:34]
4. Jika berhasil, sistem menyimpan session login. [file:34]
5. Admin diarahkan ke `/admin/artikel`. [file:34]
6. Admin dapat menambah, edit, dan hapus artikel. [file:113]
7. Admin dapat logout melalui `/user/logout`. [file:111][file:34]

---

# Potongan Kode Penting

## Routing Utama
```php
$routes->get('/', 'Home::index');
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');

$routes->get('/artikel', 'Artikel::index');
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
```
[file:111]

## Route Login dan Admin
```php
$routes->match(['get', 'post'], 'user/login', 'User::login');
$routes->get('user/logout', 'User::logout');
```
[file:111]

## Login User
```php
$login = $model->where('useremail', $email)->first();
if ($login) {
    $pass = $login['userpassword'];
    if (password_verify($password, $pass)) {
        $login_data = [
            'user_id' => $login['id'],
            'user_name' => $login['username'],
            'user_email' => $login['useremail'],
            'logged_in' => TRUE,
        ];
        $session->set($login_data);
        return redirect('admin/artikel');
    }
}
```
[file:34]

## Tambah Artikel
```php
$artikel->insert([
    'judul' => $this->request->getPost('judul'),
    'isi' => $this->request->getPost('isi'),
    'slug' => url_title($this->request->getPost('judul')),
]);
```
[file:113]

## Edit Artikel
```php
$artikel->update($id, [
    'judul' => $this->request->getPost('judul'),
    'isi' => $this->request->getPost('isi'),
]);
```
[file:113]

## Hapus Artikel
```php
$artikel->delete($id);
```
[file:113]

---

# Hasil yang Dicapai
Berdasarkan source code project, hasil yang telah dicapai antara lain:

- struktur dasar aplikasi CodeIgniter 4 sudah dibuat,
- halaman publik berhasil dibuat,
- routing berhasil diterapkan,
- artikel berhasil ditampilkan dari database,
- detail artikel sudah menggunakan slug,
- halaman admin artikel berhasil dibuat,
- fitur tambah, edit, dan hapus artikel tersedia,
- sistem login dan logout sudah dibuat,
- auth filter sudah diterapkan untuk route admin. [file:111][file:113][file:34]

---

# Kendala Project
Beberapa kendala yang masih ditemui pada project ini adalah:
- proses login admin masih perlu penyempurnaan pada beberapa pengujian,
- redirect setelah login belum selalu berjalan sesuai harapan,
- session login masih memerlukan debugging lanjutan. [file:34]

Meskipun demikian, struktur sistem sudah terbentuk dan semua komponen utama praktikum 1 sampai 4 sudah berhasil diimplementasikan dalam source code project. [file:111][file:113][file:34]

---

# Kesimpulan
Praktikum modul 1 sampai modul 4 memberikan pemahaman bertahap mengenai pengembangan web menggunakan CodeIgniter 4.  
Dimulai dari instalasi dan pengenalan framework, kemudian dilanjutkan ke pembuatan route, controller, view, integrasi database, pengelolaan artikel, hingga autentikasi login admin menggunakan session dan filter auth. Berdasarkan implementasi pada source code, project ini telah mencakup komponen utama yang dibutuhkan dalam praktikum dan dapat menjadi dasar untuk pengembangan sistem web yang lebih lengkap. [file:111][file:113][file:34]

---

# Developer
**Nama:** [Isi Nama Kamu]  
**Kelas / NIM:** [Isi Kelas atau NIM Kamu]  
**Mata Kuliah:** Praktikum Pemrograman Web / Pemrograman Web  
**Framework:** CodeIgniter 4

---
