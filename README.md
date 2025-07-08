# 🛍️ Assignment: Membangun REST API E-Commerce (Produk, Sumber, dan Transaksi)

## 🎯 Tujuan

Peserta membangun REST API sederhana menggunakan Golang dan Gin (tida wajib menggunakan database) untuk manajemen produk, sumber barang (supplier), dan transaksi penjualan. Peserta juga harus menerapkan validasi input, response JSON yang konsisten, serta testing manual menggunakan Postman atau curl.

---

## 📌 Daftar Endpoint Wajib

### 🔹 Product

1. `GET /products` – Ambil seluruh produk
2. `GET /products/:id` – Ambil produk berdasarkan ID
3. `POST /products` – Tambah produk
4. `PUT /products/:id` – Ubah produk
5. `DELETE /products/:id` – Hapus produk

**Struktur:**

```go
type Product struct {
  ID          string  `json:"id"`
  Name        string  `json:"name"`
  Description string  `json:"description"`
  Price       float64 `json:"price"`
  Stock       int     `json:"stock"`
  SourceID    string  `json:"source_id"`
}
```

---

### 🔹 Source (Supplier)

1. `GET /sources` – Ambil seluruh source
2. `GET /sources/:id` – Ambil detail source
3. `POST /sources` – Tambah source
4. `PUT /sources/:id` – Ubah source
5. `DELETE /sources/:id` – Hapus source

**Struktur:**

```go
type Source struct {
  ID   string `json:"id"`
  Name string `json:"name"`
}
```

---

### 🔹 Transaction (Simulasi Penjualan)

1. `POST /transactions` – Tambah transaksi (mengurangi stok produk)
2. `GET /transactions` – Ambil daftar transaksi
3. `GET /transactions/:id` – Ambil detail transaksi

**Struktur:**

```go
type Transaction struct {
  ID        string  `json:"id"`
  ProductID string  `json:"product_id"`
  Quantity  int     `json:"quantity"`
  Total     float64 `json:"total"`
}
```

> Saat transaksi dibuat:
>
> - Cek apakah produk ada.
> - Cek apakah `stock` mencukupi.
> - Jika cukup, kurangi stok dan buat transaksi.
> - Hitung `Total = Price * Quantity`.

---

## ✅ Requirement Teknis

- Gunakan Gin (atau explore framework lain).
- Simpan data di memory (`[]Product`, `[]Source`, `[]Transaction`).
- Validasi:

  - Produk: `price > 0`, `stock >= 0`
  - Transaksi: `quantity <= stock`, produk dan source harus valid

- Format JSON konsisten:

```json
{
  "message": "Transaction success",
  "data": {...},
  "error": null
}
```

- Status code: `200`, `201`, `400`, `404`, `500`
- Tambahkan middleware logger sederhana (opsional)

---

## 🧪 Testing & Dokumentasi

- Tes semua endpoint pakai Postman atau curl.
- Buat dokumentasi `README.md` yang berisi:

  - Daftar endpoint dan method
  - Contoh JSON request & response
  - Screenshot hasil testing

---
🧠 Bonus (Opsional)
Buat query param untuk filter produk berdasarkan nama atau sumber
GET /products?source_id=abc

Buat endpoint GET /sources/:id/products untuk melihat semua produk dari satu sumber

Simpan transaksi terakhir ke file JSON (ioutil.WriteFile)

---


# 📱 Assignment: Membangun REST API Social Media (User, Post, dan Like)

## 🎯 Tujuan

Peserta membangun REST API sederhana menggunakan Golang dan Gin (tidak wajib menggunakan database) untuk simulasi aplikasi media sosial sederhana dengan fitur user, post, dan like. Peserta juga diminta menerapkan validasi input, response JSON yang konsisten, serta testing menggunakan Postman atau curl.

---

## 📌 Daftar Endpoint Wajib

### 🔹 User

1. `POST /users` – Registrasi user baru
2. `GET /users` – Ambil semua user
3. `GET /users/:id` – Ambil profil user
4. `PUT /users/:id` – Update profil user
5. `DELETE /users/:id` – Hapus user

**Struktur:**

```go
type User struct {
  ID       string `json:"id"`
  Username string `json:"username"`
  Email    string `json:"email"`
  Bio      string `json:"bio"`
}
```

---

### 🔹 Post

1. `POST /posts` – Buat postingan baru
2. `GET /posts` – Ambil semua post
3. `GET /posts/:id` – Ambil detail post
4. `GET /users/:id/posts` – Ambil semua post dari satu user
5. `DELETE /posts/:id` – Hapus post

**Struktur:**

```go
type Post struct {
  ID      string `json:"id"`
  UserID  string `json:"user_id"`
  Content string `json:"content"`
  Created string `json:"created_at"`
}
```

---

### 🔹 Like

1. `POST /likes` – User menyukai post
2. `GET /posts/:id/likes` – Lihat siapa saja yang like post tertentu
3. `GET /users/:id/likes` – Lihat semua like dari seorang user

**Struktur:**

```go
type Like struct {
  ID     string `json:"id"`
  UserID string `json:"user_id"`
  PostID string `json:"post_id"`
}
```

---

## ✅ Requirement Teknis

* Gunakan (atau explore framework lain).
* Simpan data di memory (`[]User`, `[]Post`, `[]Like`).
* Validasi:

  * User: username dan email tidak boleh kosong
  * Post: content tidak boleh kosong, user harus valid
  * Like: satu user hanya boleh like satu post satu kali
* Format response JSON konsisten:

```json
{
  "message": "Post created successfully",
  "data": {...},
  "error": null
}
```

* Gunakan status code sesuai: `200`, `201`, `400`, `404`, `500`
* Tambahkan middleware logger atau timestamping (opsional)

---

## 🧪 Testing & Dokumentasi

* Tes endpoint menggunakan Postman atau curl.
* Buat dokumentasi `README.md` berisi:

  * Daftar endpoint dan deskripsi
  * Contoh JSON request & response
  * Screenshot hasil testing

---

## 🧠 Bonus (Opsional)

* Tambahkan komentar untuk post (`POST /comments`, `GET /posts/:id/comments`)
* Fitur follower/following antar user
* Filtering post berdasarkan user atau keyword

---

## 📅 Deadline

ditentukan oleh panitia

---

