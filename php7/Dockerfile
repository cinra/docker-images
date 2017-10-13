FROM php:7-apache

RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev libmcrypt-dev vim-athena
RUN docker-php-ext-install pdo_mysql mysqli mbstring gd iconv mcrypt

RUN a2enmod rewrite

RUN apt-get install -y ssl-cert \
  --no-install-recommends && rm -r /var/lib/apt/lists/*

COPY php.ini /usr/local/etc/php/