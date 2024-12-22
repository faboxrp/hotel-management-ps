FROM php:7.4-fpm-alpine

# Instalar dependencias necesarias
RUN apk add --no-cache \
    git \
    unzip \
    wget \
    libpng-dev \
    libjpeg-turbo-dev \
    libwebp-dev \
    libxpm-dev \
    freetype-dev \
    libxml2-dev \
    icu-dev \
    libzip-dev \
    oniguruma-dev \
    mariadb-client \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql intl zip mbstring soap \
    && rm -rf /var/cache/apk/*

# Establecer el directorio de trabajo
WORKDIR /var/www/html

# Descargar el código fuente de QloApps desde GitHub
RUN git clone --depth=1 https://github.com/Qloapps/QloApps.git .

# Configurar permisos para Apache/PHP
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

# Exponer el puerto 80
EXPOSE 80
