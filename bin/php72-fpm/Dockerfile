FROM php:7.2-fpm

RUN apt-get update && apt-get install -y \
                           libxml2-dev \
                           libcurl4-gnutls-dev \
                           libfreetype6-dev \
                           libjpeg62-turbo-dev \
                           libpng-dev \
    && docker-php-ext-install -j$(nproc) gd curl pdo_mysql opcache xml zip mbstring intl

COPY ./etc /usr/local/etc
