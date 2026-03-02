# Dockerfile (reusable base)
# Usage:
# docker build -t myphp:83-apache .
# or with Podman: podman build ...

FROM php:8.3-apache-bookworm   
# or 8.2, 8.4 — pick your main version

# Install common system deps + PHP extensions
RUN apt-get update && apt-get install -y \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip unzip git curl default-mysql-client \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo_mysql zip gd intl bcmath opcache mysqli \
    && a2enmod rewrite headers

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Optional: Xdebug for dev (can disable in php.ini later)
RUN pecl install xdebug && docker-php-ext-enable xdebug

# Custom php.ini (copy your overrides)
COPY php.ini /usr/local/etc/php/conf.d/custom.ini

# Apache config (enable .htaccess, etc.)
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

