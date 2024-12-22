# Dockerfile para QloApps basado en una imagen compatible con ARM
FROM php:7.4-apache

# Instalar dependencias necesarias
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    wget \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libxml2-dev \
    libicu-dev \
    libonig-dev \
    libzip-dev \
    zlib1g-dev \
    mariadb-client \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql intl zip mbstring soap

# Descargar y configurar QloApps
WORKDIR /var/www/html
RUN git clone --depth=1 https://github.com/Qloapps/QloApps.git .

# Configurar permisos para Apache
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

# Eliminar archivos innecesarios
RUN rm -rf /var/www/html/*

# Habilitar módulos necesarios de Apache
RUN a2enmod rewrite

# Exponer puerto 80
EXPOSE 80
