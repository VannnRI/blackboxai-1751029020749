# Panduan Download dan Deploy Sistem Administrasi Desa

## Cara 1: Download Source Code sebagai ZIP

### Langkah-langkah:
1. **Download semua file** dari direktori `village-admin/`
2. **Compress menjadi ZIP** dengan struktur folder yang sama
3. **Extract di server/komputer tujuan**

### File yang harus disertakan:
```
village-admin/
├── app/
├── bootstrap/
├── config/
├── database/
├── public/
├── resources/
├── routes/
├── storage/
├── tests/
├── .gitignore
├── .env.example
├── artisan
├── composer.json
├── composer.lock
├── package.json
├── phpunit.xml
├── README.md
├── vite.config.js
└── DEPLOYMENT_GUIDE.md
```

### Setelah Download:
1. **Install dependencies:**
   ```bash
   composer install
   ```

2. **Setup environment:**
   ```bash
   cp .env.example .env
   php artisan key:generate
   ```

3. **Setup database:**
   ```bash
   php artisan migrate:fresh --seed
   ```

4. **Jalankan aplikasi:**
   ```bash
   php artisan serve
   ```

## Cara 2: Upload ke GitHub

### Persiapan GitHub Repository:

1. **Buat repository baru di GitHub:**
   - Login ke GitHub.com
   - Klik "New repository"
   - Nama: `sistem-administrasi-desa`
   - Deskripsi: `Sistem Administrasi Desa dengan Laravel`
   - Set sebagai Public atau Private
   - Jangan centang "Initialize with README" (karena sudah ada)

2. **Initialize Git di folder project:**
   ```bash
   cd village-admin
   git init
   git add .
   git commit -m "Initial commit: Sistem Administrasi Desa"
   ```

3. **Connect ke GitHub repository:**
   ```bash
   git remote add origin https://github.com/USERNAME/sistem-administrasi-desa.git
   git branch -M main
   git push -u origin main
   ```

### Clone dari GitHub (untuk user lain):
```bash
git clone https://github.com/USERNAME/sistem-administrasi-desa.git
cd sistem-administrasi-desa
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate:fresh --seed
php artisan serve
```

## Cara 3: Deploy ke Hosting

### Shared Hosting (cPanel):

1. **Upload files** ke folder `public_html/`
2. **Pindahkan isi folder `public/`** ke root `public_html/`
3. **Edit `index.php`** di root untuk mengarah ke folder Laravel
4. **Setup database** melalui cPanel
5. **Update `.env`** dengan kredensial database hosting

### VPS/Cloud Server:

1. **Install requirements:**
   ```bash
   sudo apt update
   sudo apt install php8.2 php8.2-fpm php8.2-mysql php8.2-xml php8.2-mbstring php8.2-curl php8.2-zip
   sudo apt install nginx mysql-server composer
   ```

2. **Clone repository:**
   ```bash
   git clone https://github.com/USERNAME/sistem-administrasi-desa.git
   cd sistem-administrasi-desa
   ```

3. **Setup aplikasi:**
   ```bash
   composer install --optimize-autoloader --no-dev
   cp .env.example .env
   php artisan key:generate
   php artisan config:cache
   php artisan route:cache
   php artisan view:cache
   ```

4. **Setup database:**
   ```bash
   mysql -u root -p
   CREATE DATABASE village_admin;
   CREATE USER 'village_user'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON village_admin.* TO 'village_user'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```

5. **Update .env:**
   ```env
   APP_ENV=production
   APP_DEBUG=false
   DB_DATABASE=village_admin
   DB_USERNAME=village_user
   DB_PASSWORD=password
   ```

6. **Run migrations:**
   ```bash
   php artisan migrate:fresh --seed
   ```

7. **Setup permissions:**
   ```bash
   sudo chown -R www-data:www-data storage bootstrap/cache
   sudo chmod -R 775 storage bootstrap/cache
   ```

## Konfigurasi Nginx (untuk VPS):

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /path/to/village-admin/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

## Troubleshooting

### Error Permission:
```bash
sudo chmod -R 775 storage bootstrap/cache
sudo chown -R www-data:www-data storage bootstrap/cache
```

### Error Composer:
```bash
composer install --ignore-platform-reqs
```

### Error Database:
- Pastikan kredensial database benar di `.env`
- Pastikan database sudah dibuat
- Jalankan `php artisan migrate:fresh --seed`

### Error Key:
```bash
php artisan key:generate
```

## Akun Default

Setelah seeding database, gunakan akun berikut:

**Super Admin:**
- Email: admin@admin.com
- Password: admin

**Admin Desa:**
- Email: desa@admin.com
- Password: password

**Staff Desa:**
- Email: staff@admin.com
- Password: password

**Masyarakat:**
- NIK: 3374121234567890
- Password: 1990-01-01

## Backup Database

### Export:
```bash
mysqldump -u username -p village_admin > backup.sql
```

### Import:
```bash
mysql -u username -p village_admin < backup.sql
```

## Update Aplikasi

```bash
git pull origin main
composer install
php artisan migrate
php artisan config:cache
php artisan route:cache
php artisan view:cache
