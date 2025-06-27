# Instruksi Download Sistem Administrasi Desa

## 📁 File yang Tersedia untuk Download

### 1. Source Code Lengkap (Compressed)
- **File**: `sistem-administrasi-desa.tar.gz` (92 KB)
- **Lokasi**: `/project/sandbox/user-workspace/sistem-administrasi-desa.tar.gz`
- **Isi**: Semua source code kecuali vendor, node_modules, dan file environment

### 2. Folder Project Lengkap
- **Folder**: `village-admin/`
- **Lokasi**: `/project/sandbox/user-workspace/village-admin/`
- **Isi**: Semua file project termasuk database dan dependencies

## 🚀 Cara Download dan Setup

### Opsi 1: Download File Compressed
1. **Download** file `sistem-administrasi-desa.tar.gz`
2. **Extract** di komputer/server tujuan:
   ```bash
   tar -xzf sistem-administrasi-desa.tar.gz
   cd village-admin
   ```
3. **Install dependencies**:
   ```bash
   composer install
   ```
4. **Setup environment**:
   ```bash
   cp .env.example .env
   php artisan key:generate
   ```
5. **Setup database**:
   ```bash
   php artisan migrate:fresh --seed
   ```
6. **Jalankan aplikasi**:
   ```bash
   php artisan serve
   ```

### Opsi 2: Copy Folder Lengkap
1. **Copy** seluruh folder `village-admin/`
2. **Pindahkan** ke lokasi tujuan
3. **Langsung jalankan** (jika dependencies sudah ada):
   ```bash
   cd village-admin
   php artisan serve
   ```

## 📋 Struktur File yang Akan Anda Dapatkan

```
village-admin/
├── 📁 app/                     # Core aplikasi
│   ├── 📁 Http/
│   │   ├── 📁 Controllers/     # Controllers
│   │   └── 📁 Middleware/      # Middleware
│   └── 📁 Models/              # Models database
├── 📁 database/                # Database & migrations
│   ├── 📁 migrations/          # File migrasi
│   └── 📁 seeders/             # Data awal
├── 📁 resources/               # Views & assets
│   └── 📁 views/               # Template Blade
│       ├── 📁 auth/            # Halaman login
│       ├── 📁 super-admin/     # Dashboard super admin
│       ├── 📁 village-admin/   # Dashboard admin desa
│       ├── 📁 village-staff/   # Dashboard staff desa
│       └── 📁 citizen/         # Dashboard masyarakat
├── 📁 routes/                  # Routing
├── 📁 config/                  # Konfigurasi
├── 📁 public/                  # File publik
├── 📄 README.md                # Dokumentasi lengkap
├── 📄 DEPLOYMENT_GUIDE.md      # Panduan deploy
└── 📄 .env.example             # Template environment
```

## 🔐 Akun Default untuk Testing

Setelah setup selesai, gunakan akun berikut:

### Super Admin
- **Email**: admin@admin.com
- **Password**: admin
- **Akses**: Kelola semua desa dan akun

### Admin Desa
- **Email**: desa@admin.com
- **Password**: password
- **Akses**: Kelola data penduduk, surat, arsip

### Staff Desa
- **Email**: staff@admin.com
- **Password**: password
- **Akses**: Validasi surat masyarakat

### Masyarakat
- **NIK**: 3374121234567890
- **Password**: 1990-01-01
- **Akses**: Ajukan surat, lihat status

## 🌐 Upload ke GitHub

### Langkah-langkah:
1. **Buat repository baru** di GitHub
2. **Initialize Git**:
   ```bash
   cd village-admin
   git init
   git add .
   git commit -m "Initial commit: Sistem Administrasi Desa"
   ```
3. **Connect ke GitHub**:
   ```bash
   git remote add origin https://github.com/USERNAME/REPO-NAME.git
   git branch -M main
   git push -u origin main
   ```

### Clone dari GitHub:
```bash
git clone https://github.com/USERNAME/REPO-NAME.git
cd REPO-NAME
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate:fresh --seed
php artisan serve
```

## 🛠️ Fitur Utama Sistem

### ✅ Multi-Role Authentication
- Super Admin, Admin Desa, Staff Desa, Masyarakat

### ✅ Manajemen Penduduk
- Data NIK, KK, nama, tanggal lahir, alamat

### ✅ Sistem Surat Menyurat
- Pengajuan surat oleh masyarakat
- Validasi oleh staff desa
- Download surat yang disetujui

### ✅ Arsip Administrasi
- Administrasi umum
- Administrasi penduduk
- Administrasi surat menyurat

### ✅ Website Desa
- Konten dapat dikelola admin desa
- Tampilan untuk masyarakat

### ✅ Dashboard Role-Based
- Interface berbeda untuk setiap role
- Statistik dan laporan

## 📞 Support

Jika ada pertanyaan atau masalah:
1. Baca file `README.md` untuk dokumentasi lengkap
2. Baca file `DEPLOYMENT_GUIDE.md` untuk panduan deploy
3. Periksa file `.env.example` untuk konfigurasi environment

## 📝 Teknologi yang Digunakan

- **Backend**: Laravel 12.x (PHP 8.2+)
- **Database**: MySQL/SQLite
- **Frontend**: Blade Templates + Tailwind CSS
- **Authentication**: Laravel Auth
- **Styling**: Tailwind CSS + Google Fonts

---

**Sistem Administrasi Desa** - Solusi digital untuk administrasi desa modern
