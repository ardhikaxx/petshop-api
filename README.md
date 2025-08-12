---

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
   git clone https://github.com/ardhikaxx/petshop-api.git
   cd petshop-api
    ```

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

## 📦 Storage Setup

To handle product image storage:

1. Create the storage link (this will create a symbolic link from `public/storage` to `storage/app/public`):
   ```bash
   php artisan storage:link
   ```

2. Ensure your `.env` has these settings:
   ```env
   FILESYSTEM_DISK=public
   ```

3. The images will be stored in:
   ```
   storage/app/public/products
   ```
   And accessible via:
   ```
   http://your-domain/storage/products/filename.jpg
   ```

## 🔗 Endpoint API

### Base URL
```
http://localhost:8000/api
```

### Products Endpoints

| Method | Endpoint         | Description                |
|--------|------------------|----------------------------|
| GET    | /products        | Get all products           |
| POST   | /products        | Create a new product       |
| GET    | /products/{id}   | Get a specific product     |
| PUT    | /products/{id}   | Update a product           |
| DELETE | /products/{id}   | Delete a product           |

## Request & Response Examples

### 1. Get All Products
**Request:**
```
GET /api/products
```

**Response (Success):**
```json
{
  "status": "success",
  "data": [
    {
      "id": 1,
      "name": "Cat Food",
      "description": "Premium quality cat food",
      "price": 15.99,
      "stock": 50,
      "image": "products/cat-food.jpg",
      "category": "food",
      "created_at": "2023-08-12T10:00:00.000000Z",
      "updated_at": "2023-08-12T10:00:00.000000Z",
      "image_url": "http://localhost/storage/products/cat-food.jpg"
    }
  ],
  "message": "Products retrieved successfully"
}
```

### 2. Create a Product
**Request:**
```
POST /api/products
Headers:
  Content-Type: multipart/form-data
  Accept: application/json

Body:
  name: Dog Food
  description: Nutritious dog food
  price: 19.99
  stock: 30
  category: food
  image: [file]
```

**Response (Success):**
```json
{
  "status": "success",
  "data": {
    "id": 2,
    "name": "Dog Food",
    "description": "Nutritious dog food",
    "price": 19.99,
    "stock": 30,
    "image": "products/dog-food.jpg",
    "category": "food",
    "created_at": "2023-08-12T10:05:00.000000Z",
    "updated_at": "2023-08-12T10:05:00.000000Z",
    "image_url": "http://localhost/storage/products/dog-food.jpg"
  },
  "message": "Product created successfully"
}
```

### 3. Update a Product
**Request:**
```
PUT /api/products/2
Headers:
  Content-Type: multipart/form-data
  Accept: application/json

Body:
  name: Premium Dog Food
  price: 24.99
```

**Response (Success):**
```json
{
  "status": "success",
  "data": {
    "id": 2,
    "name": "Premium Dog Food",
    "description": "Nutritious dog food",
    "price": 24.99,
    "stock": 30,
    "image": "products/dog-food.jpg",
    "category": "food",
    "created_at": "2023-08-12T10:05:00.000000Z",
    "updated_at": "2023-08-12T10:10:00.000000Z",
    "image_url": "http://localhost/storage/products/dog-food.jpg"
  },
  "message": "Product updated successfully"
}
```

### 4. Delete a Product
**Request:**
```
DELETE /api/products/2
```

**Response (Success):**
```json
{
  "status": "success",
  "message": "Product deleted successfully"
}
```