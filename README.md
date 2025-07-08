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
