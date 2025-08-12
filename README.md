---

````markdown
# Petshop API - Product Management

Petshop API adalah projek berbasis Laravel yang menyediakan endpoint untuk mengelola data produk, termasuk upload gambar dengan penyimpanan di `storage/public` yang dapat diakses publik.

---

## 📌 Fitur Utama

- CRUD (Create, Read, Update, Delete) produk.
- Upload gambar produk dan simpan di `storage/app/public/products`.
- Validasi data input.
- Menyediakan response dalam format JSON.
- Akses gambar langsung via URL setelah `php artisan storage:link`.

---

## 📦 Instalasi & Persiapan

1. **Clone Repository**
   ```bash
   git clone https://github.com/username/petshop-api.git
   cd petshop-api
````

2. **Install Dependency**

   ```bash
   composer install
   ```

3. **Buat File `.env`**

   ```bash
   cp .env.example .env
   ```

4. **Generate App Key**

   ```bash
   php artisan key:generate
   ```

5. **Konfigurasi Database**
   Edit file `.env`:

   ```
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=petshop_api
    DB_USERNAME=root
    DB_PASSWORD=
   ```

6. **Migrasi Database**

   ```bash
   php artisan migrate
   ```

7. **Buat Storage Link** (untuk akses gambar)

   ```bash
   php artisan storage:link
   ```

8. **Jalankan Server**

   ```bash
   php artisan serve
   ```

---

## 🔗 Endpoint API

### 1. **Get All Products**

* **URL:** `/api/products`
* **Method:** `GET`
* **Response:**

```json
{
    "status": "success",
    "data": [
        {
            "id": 1,
            "name": "Dog Food",
            "description": "Premium dog food",
            "price": "150000.00",
            "stock": 50,
            "image": "products/dogfood.jpg",
            "category": "Food",
            "created_at": "2025-08-12T07:00:00.000000Z",
            "updated_at": "2025-08-12T07:00:00.000000Z"
        }
    ],
    "message": "Products retrieved successfully"
}
```

---

### 2. **Create Product**

* **URL:** `/api/products`

* **Method:** `POST`

* **Headers:**
  `Content-Type: multipart/form-data`

* **Body:**
  \| Field        | Tipe Data  | Wajib | Keterangan                              |
  \|--------------|------------|-------|-----------------------------------------|
  \| name         | string     | ✅    | Nama produk                             |
  \| description  | string     | ✅    | Deskripsi produk                        |
  \| price        | numeric    | ✅    | Harga produk                            |
  \| stock        | integer    | ✅    | Stok produk                             |
  \| category     | string     | ✅    | Kategori produk                         |
  \| image        | file       | ❌    | Gambar produk (jpeg,png,jpg,gif, max 2MB) |

* **Contoh Request (cURL):**

```bash
curl -X POST http://localhost:8000/api/products \
  -F "name=Dog Food" \
  -F "description=Premium dog food" \
  -F "price=150000" \
  -F "stock=50" \
  -F "category=Food" \
  -F "image=@/path/to/dogfood.jpg"
```

---

### 3. **Get Product By ID**

* **URL:** `/api/products/{id}`
* **Method:** `GET`
* **Response jika ditemukan:**

```json
{
    "status": "success",
    "data": {
        "id": 1,
        "name": "Dog Food",
        "description": "Premium dog food",
        "price": "150000.00",
        "stock": 50,
        "image": "products/dogfood.jpg",
        "category": "Food",
        "created_at": "2025-08-12T07:00:00.000000Z",
        "updated_at": "2025-08-12T07:00:00.000000Z"
    },
    "message": "Product retrieved successfully"
}
```

* **Response jika tidak ditemukan:**

```json
{
    "status": "error",
    "message": "Product not found"
}
```

---

### 4. **Update Product**

* **URL:** `/api/products/{id}`

* **Method:** `PUT`

* **Headers:**
  `Content-Type: multipart/form-data`

* **Body:** (semua field opsional, sama seperti create)

* **Catatan:**

  * Jika mengupload gambar baru, gambar lama akan dihapus otomatis.
  * Gunakan method `PUT` untuk update.

* **Contoh Request (cURL):**

```bash
curl -X PUT http://localhost:8000/api/products/1 \
  -F "name=Updated Dog Food" \
  -F "price=200000" \
  -F "image=@/path/to/newimage.jpg"
```

---

### 5. **Delete Product**

* **URL:** `/api/products/{id}`
* **Method:** `DELETE`
* **Response jika berhasil:**

```json
{
    "status": "success",
    "message": "Product deleted successfully"
}
```

* **Catatan:**

  * Gambar yang terkait produk akan dihapus dari storage.

---

## 🖼️ Akses Gambar

Gambar tersimpan di folder `storage/app/public/products`.
Setelah menjalankan:

```bash
php artisan storage:link
```

Gambar dapat diakses melalui URL:

```
http://localhost:8000/storage/products/namafile.jpg
```

---

## 🧪 Testing API dengan Postman

1. Import endpoint ke Postman.
2. Gunakan URL `http://localhost:8000/api`.
3. Sesuaikan method dan body sesuai dokumentasi di atas.

---

## 📚 Tentang Laravel

Laravel adalah framework aplikasi web dengan sintaks yang ekspresif dan elegan.
Pelajari lebih lanjut di [Laravel Documentation](https://laravel.com/docs).

---

## 📄 Lisensi

Proyek ini menggunakan [MIT License](https://opensource.org/licenses/MIT).

```

---

Kalau mau, aku bisa buatkan **file `.json` Postman Collection** supaya tinggal di-import dan langsung bisa testing semua endpoint.  
Kalau setuju, nanti aku sertakan di repo kamu biar praktis.
```
