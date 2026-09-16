FROM php:8.3-fpm-alpine

RUN apk update && apk upgrade
RUN apk add mc

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo pdo_mysql
# Install pcntl - manage processes
RUN docker-php-ext-configure pcntl --enable-pcntl && docker-php-ext-install pcntl

WORKDIR /var/www
