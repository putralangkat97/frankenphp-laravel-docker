FROM dunglas/frankenphp:php8.4-alpine

ENV SERVER_NAME=:80

WORKDIR /app

COPY . /app

RUN apk add --no-cache \
    zip \
    libzip-dev \
    git \
    unzip \
    icu-dev

RUN install-php-extensions \
    pdo_pgsql \
    intl \
    zip \
    opcache

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN composer install --no-interaction --prefer-dist
