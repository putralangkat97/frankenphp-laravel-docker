<p align="center">
  <a href="https://laravel.com" target="_blank">
    <img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo">
  </a>
</p>

<p align="center">
  <a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
  <a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
  <a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
  <a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

# Laravel + FrankenPHP Dev Stack (Docker Compose)

## English

Template-ready Laravel development environment powered by **FrankenPHP (Caddy)** and Docker Compose.  
Choose one database: **MariaDB**, **MySQL**, or **PostgreSQL**. Includes **Redis** and a DB admin UI (**phpMyAdmin** for MariaDB/MySQL, **pgAdmin** for PostgreSQL).

### What's inside

- Laravel + FrankenPHP (Caddy)
- Redis
- MariaDB + phpMyAdmin (default), or MySQL + phpMyAdmin, or PostgreSQL + pgAdmin

---

## Indonesia

Template environment development Laravel dengan **FrankenPHP (Caddy)** dan Docker Compose.  
Pilih salah satu database: **MariaDB**, **MySQL**, atau **PostgreSQL**. Termasuk **Redis** dan UI admin DB (**phpMyAdmin** untuk MariaDB/MySQL, **pgAdmin** untuk PostgreSQL).

### Isi stack

- Laravel + FrankenPHP (Caddy)
- Redis
- MariaDB + phpMyAdmin (default), atau MySQL + phpMyAdmin, atau PostgreSQL + pgAdmin

---

## Quick start (MariaDB default)

```bash
docker compose up -d --build
docker compose exec laravel_franken php artisan key:generate
docker compose exec laravel_franken php artisan migrate
```

Open:

- App: http://localhost:8001
- phpMyAdmin: http://localhost:8080

---

## Switch database

### Option A — MariaDB (default)

Ensure `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=mariadb
DB_PORT=3306
REDIS_HOST=redis
```

Run:

```bash
docker compose up -d --build
```

### Option B — MySQL

1. Edit `docker-compose.yml`:

- In `laravel_franken`:
    - `image: laravel-orbstack/mysql`
    - `dockerfile: docker/mysql/Dockerfile`
    - `depends_on: - mysql`
- Uncomment service `mysql`
- In `phpmyadmin`, set:
    - `PMA_HOST: mysql`
    - `depends_on: - mysql`
- Comment out service `mariadb`

2. Ensure `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
REDIS_HOST=redis
```

Run:

```bash
docker compose up -d --build
```

### Option C — PostgreSQL

1. Edit `docker-compose.yml`:

- In `laravel_franken`:
    - `image: laravel-orbstack/postgres`
    - `dockerfile: docker/postgres/Dockerfile`
    - `depends_on: - postgres`
- Uncomment services `postgres` and `pgadmin`
- Comment out `mariadb`, `mysql`, and `phpmyadmin`

2. Ensure `.env`:

```env
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
REDIS_HOST=redis
```

Run:

```bash
docker compose up -d --build
```

Open:

- App: http://localhost:8001
- pgAdmin: http://localhost:5050

---

## Common commands

**Build images**

```bash
docker compose build --no-cache
```

**Logs**

```bash
docker compose logs -f
```

**Shell / Artisan**

```bash
docker compose exec laravel_franken sh
docker compose exec laravel_franken php artisan
```

**Stop**

```bash
docker compose down
```

---

## Notes

- `php artisan` should be run inside the container (via `docker compose exec`) so service hostnames like `mariadb/mysql/postgres/redis` resolve correctly.
- If you change `.env`, clear config cache:

```bash
docker compose exec laravel_franken php artisan config:clear
```

Laravel: https://laravel.com
