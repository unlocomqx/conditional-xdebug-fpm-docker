FROM php:8.2-fpm

RUN apt-get update && apt-get install -y \
    libxml2-dev \
    libcurl4-gnutls-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libmemcached-dev \
    libzip-dev \
    libonig-dev \
    libicu-dev \
    && docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg=/usr/local/lib --with-webp \
    && docker-php-ext-install -j$(nproc) gd curl pdo_mysql mysqli opcache xml zip mbstring intl

RUN pecl install -f xdebug-3.2.0 && \
    docker-php-ext-enable xdebug

RUN apt-get install -y libmagickwand-dev --no-install-recommends \
    && pecl install imagick \
	&& docker-php-ext-enable imagick

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY ./etc /usr/local/etc
