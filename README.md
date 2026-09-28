# 🐳 Stack WordPress + Nginx + Adminer con Docker

![Docker Logo](https://www.docker.com/app/uploads/2023/08/logo-guide-logos-1.svg)

Este proyecto levanta un entorno completo de **WordPress** utilizando **Docker Compose**, ideal para desarrollo local o pruebas rápidas.

##  Contenido de los Servicios

- **WordPress (PHP-FPM 8.2)**  
  Ejecuta WordPress con PHP-FPM 8.2. Los archivos del sitio se guardan en: `./wp-data`.

- **Nginx (stable)**  
  Servidor frontend que expone WordPress en **[http://localhost:8080](http://localhost:8080)**. Usa configuración personalizada (`./nginx/default.conf`).

- **MariaDB (10.6)**  
  Base de datos para WordPress, con datos persistentes en el volumen `db_data`.  

  ⚠️ **Importante**: debes configurar tus propios valores de conexión en el archivo `docker-compose.yml`.  
  Los que vienen son solo de ejemplo:  
  - Usuario: `wpuser`  
  - Contraseña: `wppass`  
  - Base de datos: `wpdb`  
  - Root: `rootpass`  


- **Adminer**  
  Interfaz web para gestionar la base de datos en **[http://localhost:8081](http://localhost:8081)**. Usa tema CSS personalizado (`./adminer-theme/adminer.css`).

## ▶ Cómo usarlo

Requisitos: Docker + Docker Compose (v2, `docker compose`).

1. Clona el repositorio:
   ```bash
   git clone https://github.com/nahataen/docker-wp-nginx-adminer.git
   cd docker-wp-nginx-adminer
   ```

2. (Opcional) Ajusta usuarios y contraseñas de ejemplo en `docker-compose.yml`
   (`wpuser` / `wppass` / `wpdb` / `rootpass`).

3. Levanta el stack:
   ```bash
   docker compose up -d
   docker compose ps
   ```

4. Abre:
   - WordPress (vía Nginx): [http://localhost:8080](http://localhost:8080)
   - Adminer: [http://localhost:8081](http://localhost:8081) (motor `db`, usuario/clave del compose)

5. Para detenerlo:
   ```bash
   docker compose down
   # con datos: docker compose down -v
   ```

## Servicios (`docker-compose.yml`)

| Servicio | Imagen | Puerto | Notas |
|---|---|---|---|
| `wordpress` | `wordpress:php8.2-fpm` | — (interno) | Archivos en `./wp-data` |
| `nginx` | `nginx:stable` | `8080:80` | Config `./nginx/default.conf` |
| `db` | `mariadb:10.6` | — (interno) | Datos en volumen `db_data` |
| `adminer` | `adminer` | `8081:8080` | Tema `./adminer-theme/adminer.css` |
