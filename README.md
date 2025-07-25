# README

Create the dockerfile such as "dockerfile" with the following content:

```bash
FROM php:8.3

# Instalar dependencias
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    unzip \
    default-mysql-client

# Limpiar cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Instalar extensiones PHP
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Configurar directorio de trabajo
WORKDIR /var/www/html
```

Create the image with the following command:

```bash
docker build -t my-php-gp .
```