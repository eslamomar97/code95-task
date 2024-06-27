# Task 1: Dockerized WordPress with Nginx, PHP-FPM 8.2, and MySQL 8

This repository contains a Docker Compose configuration for setting up WordPress with Nginx, PHP-FPM 8.2, and MySQL 8 in the Task1 folder.

## Prerequisites

- Docker
- Docker Compose

## Getting Started


### Nginx Configuration

Create an Nginx configuration file at `nginx/conf.d/default.conf`:

```nginx
server {
    listen 80;
    server_name firtswebsite.com;

    root /var/www/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
	    include fastcgi_params;
        fastcgi_pass wordpress:9000;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }
}
```
Ensure you are in the directory containing the `docker-compose.yml` file.

**Configuration**

- **MySQL Database:**
  - Host: `db:3306`
  - Database: `wordpress`
  - Username: `wordpressuser`
  - Password: `wordpresspassword`

- **WordPress Admin:**
  - Access your WordPress admin panel at [http://localhost:8080/wp-admin](http://localhost:8080/wp-admin).
  - Log in with the credentials set during the WordPress installation.

- **phpMyAdmin:**
  - Access phpMyAdmin at [http://localhost:8082](http://localhost:8082) with MySQL root credentials:
    - Username: `root`
    - Password: `rootpassword`

**Notes**

- Make sure ports `8080`, `8082` are available on your host machine and not already used by other services.
- This setup uses Docker volumes for persistent storage of MySQL and WordPress data.

Start the Docker containers:

```bash
docker-compose up -d
```

**Access WordPress:**

- WordPress site: [http://localhost:8080](http://localhost:8080)
- phpMyAdmin (for database management): [http://localhost:8082](http://localhost:8082)

**Stop the Docker containers:**
```bash
docker-compose down
```
