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

## Change to working directory

```bash
cd /Users/my-user/Desktop/git/repository
docker run --rm -it -v $PWD:/app -u $(id -u):$(id -g) composer:2.8.0 composer install
```

## Run the container

```bash
docker run --rm -it -v $PWD:/var/www/html -p 8000:8000 <docker-image> php artisan serve --host=0.0.0.0 --port=8000

# Recommended to use the image created above
docker run --rm -it -v $PWD:/var/www/html -p 8000:8000 my-php-gp php artisan serve --host=0.0.0.0 --port=8000
```