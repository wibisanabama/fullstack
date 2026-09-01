# Fullstack API

REST API untuk autentikasi pengguna dan pengelolaan post. Repository saat ini hanya berisi backend Laravel. Frontend React belum tersedia.

## Technology Stack

- PHP 8.2 atau lebih baru
- Laravel 11
- Laravel Sanctum
- MySQL
- Node.js dan Vite

## Project Structure

```text
fullstack/
├── backend/    Laravel REST API
└── README.md
```

## Requirements

Pastikan perangkat telah memiliki:

- PHP 8.2+
- Composer
- MySQL
- Node.js dan npm

## Installation

Masuk ke direktori backend dan pasang dependensi:

```bash
cd backend
composer install
npm install
```

Buat konfigurasi environment:

```bash
cp .env.example .env
php artisan key:generate
```

Sesuaikan koneksi database pada `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=backend
DB_USERNAME=root
DB_PASSWORD=
```

Buat database sesuai nilai `DB_DATABASE`, lalu jalankan migration:

```bash
php artisan migrate
```

## Running the Application

Jalankan seluruh proses development:

```bash
composer run dev
```

API tersedia secara default di `http://127.0.0.1:8000/api`.

Untuk menjalankan server API saja:

```bash
php artisan serve
```

## Authentication

Endpoint yang dilindungi menggunakan Sanctum bearer token. Kirim token pada setiap request terautentikasi:

```http
Authorization: Bearer <token>
Accept: application/json
```

Token diberikan oleh endpoint register dan login.

## API Endpoints

| Method | Endpoint | Authentication | Description |
| --- | --- | --- | --- |
| POST | `/api/register` | Tidak | Membuat akun dan token |
| POST | `/api/login` | Tidak | Login dan membuat token |
| POST | `/api/logout` | Ya | Menghapus token pengguna |
| GET | `/api/user` | Ya | Mengambil pengguna aktif |
| GET | `/api/posts` | Tidak | Mengambil semua post |
| GET | `/api/posts/{post}` | Tidak | Mengambil satu post |
| POST | `/api/posts` | Ya | Membuat post |
| PUT/PATCH | `/api/posts/{post}` | Pemilik post | Memperbarui post |
| DELETE | `/api/posts/{post}` | Pemilik post | Menghapus post |

## Request Fields

Register:

```json
{
  "name": "Example User",
  "email": "user@example.com",
  "password": "password",
  "password_confirmation": "password"
}
```

Login:

```json
{
  "email": "user@example.com",
  "password": "password"
}
```

Create or update post:

```json
{
  "title": "Post title",
  "body": "Post content"
}
```

## Testing

```bash
php artisan test
```
