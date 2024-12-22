# Dockerfile para QloApps basado en la imagen oficial de PrestaShop
FROM prestashop/prestashop:1.6.1.23

# Cambiar los repositorios de Debian Stretch a los archivados y eliminar stretch-updates
RUN sed -i 's|http://deb.debian.org/debian|http://archive.debian.org/debian|g' /etc/apt/sources.list && \
    sed -i 's|http://security.debian.org/debian-security|http://archive.debian.org/debian-security|g' /etc/apt/sources.list && \
    sed -i '/stretch-updates/d' /etc/apt/sources.list && \
    echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid-until

# Instalar dependencias necesarias (incluyendo git)
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Descargar y configurar QloApps
WORKDIR /var/www/html

# Eliminar el contenido predeterminado de PrestaShop
RUN rm -rf /var/www/html/*

# Descargar el código de QloApps desde GitHub directamente
RUN git clone --depth=1 https://github.com/Qloapps/QloApps.git /var/www/html

# Configurar permisos para Apache
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

# Habilitar módulos de Apache necesarios
RUN a2enmod rewrite
