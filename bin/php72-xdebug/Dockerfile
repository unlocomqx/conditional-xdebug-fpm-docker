FROM php:7.2-fpm

RUN apt-get update && apt-get install -y \
    libxml2-dev \
    libcurl4-gnutls-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmemcached-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd curl pdo_mysql opcache xml zip mbstring intl

RUN pecl install -f xdebug && \
    docker-php-ext-enable xdebug

RUN pecl install -f memcached && \
    docker-php-ext-enable memcached

COPY ./etc /usr/local/etc
