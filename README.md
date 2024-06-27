# Task 1: # Dockerized WordPress with Nginx, PHP-FPM 8.2, and MySQL 8

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
    server_name yourdomain.com;

    root /var/www/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass php-fpm:9000;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }
}
```
Ensure you are in the directory containing the `docker-compose.yml` file.

Start the Docker containers:

```bash
docker-compose up -d
```

```bash
docker-compose up -d
Open your web browser and navigate to http://localhost to complete the WordPress setup.
```

