# Event Management

Aplikasi sistem manajemen event berbasis **Laravel (Backend API)** dan **React + Vite (Frontend)**.

---

## Prasyarat

Pastikan perangkat kamu sudah terinstal:

- PHP >= 8.2
- Composer
- Node.js >= 18 & npm
- MySQL
- Git

---

## Struktur Proyek

```
event-management/
├── app/                  # Backend Laravel
├── database/
├── routes/
├── frontend/             # Frontend React + Vite
│   ├── src/
│   └── package.json
├── .env.example
└── ...
```

---

## Instalasi Backend (Laravel)

### 1. Clone Repository

```bash
git clone https://github.com/far-abhipraya/event-management.git
cd event-management
```

### 2. Install Dependensi PHP

```bash
composer install
```

### 3. Konfigurasi File `.env`

Salin file `.env.example` menjadi `.env`:

```bash
cp .env.example .env
```

Kemudian edit file `.env` dan sesuaikan konfigurasi berikut:

```env
APP_NAME="Event Management"
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost:8000

# Konfigurasi Database — ganti sesuai MySQL kamu
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=event_management
DB_USERNAME=root
DB_PASSWORD=

# Konfigurasi JWT
JWT_SECRET=
```

> **Catatan:**
> - `DB_DATABASE` diisi nama database MySQL yang akan digunakan (buat terlebih dahulu jika belum ada).
> - `DB_USERNAME` dan `DB_PASSWORD` disesuaikan dengan kredensial MySQL lokal kamu.
> - `JWT_SECRET` akan di-generate otomatis pada langkah berikutnya.

### 4. Generate Application Key & JWT Secret

```bash
php artisan key:generate
php artisan jwt:secret
```

### 5. Buat Database

Buat database baru di MySQL dengan nama sesuai `DB_DATABASE` di `.env`:

```sql
CREATE DATABASE event_management;
```

### 6. Jalankan Migration & Seeder

```bash
php artisan migrate:fresh --seed
```

Perintah ini akan membuat semua tabel dan mengisi data dummy ke database.

### 7. Jalankan Backend Server

```bash
php artisan serve
```

Backend API akan berjalan di: **`http://localhost:8000`**

---

## Instalasi Frontend (React + Vite)

### 1. Masuk ke Folder Frontend

```bash
cd frontend
```

### 2. Install Dependensi Node

```bash
npm install
```

### 3. Jalankan Frontend Dev Server

```bash
npm run dev
```

Frontend akan berjalan di: **`http://localhost:5173`**

> Pastikan backend Laravel sudah berjalan di `http://localhost:8000` sebelum menjalankan frontend.

---

## Menjalankan Aplikasi Lengkap

Buka **dua terminal** secara bersamaan:

**Terminal 1 — Backend:**
```bash
# dari root folder event-management/
php artisan serve
```

**Terminal 2 — Frontend:**
```bash
# dari folder event-management/frontend/
cd frontend
npm run dev
```

Akses aplikasi di browser: **`http://localhost:5173`**

---

## Daftar Endpoint API

Base URL: `http://localhost:8000/api`

### Authentication (Public)

| Method | Endpoint | Keterangan |
|--------|----------|------------|
| POST | `/auth/register` | Registrasi akun baru |
| POST | `/auth/login` | Login dan mendapatkan token JWT |

### Authentication (Protected)

| Method | Endpoint | Keterangan |
|--------|----------|------------|
| POST | `/auth/logout` | Logout |
| GET | `/auth/profile` | Lihat profil user yang login |

### Events

| Method | Endpoint | Role | Keterangan |
|--------|----------|------|------------|
| GET | `/events` | Semua | Daftar semua event |
| GET | `/events/{id}` | Semua | Detail event |
| POST | `/events` | admin, organizer | Tambah event baru |
| PUT | `/events/{id}` | admin, organizer | Update event |
| DELETE | `/events/{id}` | admin | Hapus event |

### Organizers

| Method | Endpoint | Role | Keterangan |
|--------|----------|------|------------|
| GET | `/organizers` | Semua | Daftar organizer |
| GET | `/organizers/{id}` | Semua | Detail organizer |
| POST | `/organizers` | admin | Tambah organizer |
| PUT | `/organizers/{id}` | admin | Update organizer |
| DELETE | `/organizers/{id}` | admin | Hapus organizer |

### Venues

| Method | Endpoint | Role | Keterangan |
|--------|----------|------|------------|
| GET | `/venues` | Semua | Daftar venue |
| GET | `/venues/{id}` | Semua | Detail venue |
| POST | `/venues` | admin, organizer | Tambah venue |
| PUT | `/venues/{id}` | admin, organizer | Update venue |
| DELETE | `/venues/{id}` | admin | Hapus venue |

### Tags

| Method | Endpoint | Role | Keterangan |
|--------|----------|------|------------|
| GET | `/tags` | Semua | Daftar tag |
| GET | `/tags/{id}` | Semua | Detail tag |
| POST | `/tags` | admin, organizer | Tambah tag |
| PUT | `/tags/{id}` | admin, organizer | Update tag |
| DELETE | `/tags/{id}` | admin | Hapus tag |

### Participants

| Method | Endpoint | Role | Keterangan |
|--------|----------|------|------------|
| GET | `/participants` | Semua | Daftar peserta |
| GET | `/participants/{id}` | Semua | Detail peserta |
| POST | `/participants` | admin, organizer, participant | Tambah peserta |
| PUT | `/participants/{id}` | admin | Update peserta |
| DELETE | `/participants/{id}` | admin | Hapus peserta |

### Registrations

| Method | Endpoint | Role | Keterangan |
|--------|----------|------|------------|
| GET | `/registrations` | Semua | Daftar registrasi |
| GET | `/registrations/{id}` | Semua | Detail registrasi |
| POST | `/registrations` | admin, organizer, participant | Tambah registrasi |
| PUT | `/registrations/{id}` | admin, organizer | Update registrasi |
| DELETE | `/registrations/{id}` | admin | Hapus registrasi |

> Semua endpoint di atas (selain `/auth/register` dan `/auth/login`) membutuhkan header:
> ```
> Authorization: Bearer {token}
> ```

---

## Tech Stack

| Layer | Teknologi |
|-------|----------|
| Backend | Laravel, PHP, MySQL, JWT Auth |
| Frontend | React 19, React Router DOM, Axios, Vite |

---

## Lisensi

Proyek ini dibuat untuk keperluan akademik — Ujian Tengah Praktikum (UTP) dan Ujian Akhir Praktikum (UAP).
