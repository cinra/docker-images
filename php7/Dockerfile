FROM php:7.2.3-apache

RUN apt-get update && \
    apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev vim-athena
RUN docker-php-ext-install pdo_mysql mysqli mbstring gd iconv

RUN pecl install mcrypt-1.0.1 xdebug
RUN docker-php-ext-enable mcrypt xdebug

RUN echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN a2enmod rewrite

RUN apt-get install -y ssl-cert \
  --no-install-recommends && rm -r /var/lib/apt/lists/*

COPY php.ini /usr/local/etc/php/