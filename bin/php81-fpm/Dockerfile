FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
    libxml2-dev \
    libcurl4-gnutls-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmemcached-dev \
    libzip-dev \
    libonig-dev \
    && docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg=/usr/local/lib \
    && docker-php-ext-install -j$(nproc) gd curl pdo_mysql mysqli opcache xml zip mbstring intl

COPY ./etc /usr/local/etc
