FROM php:8.2-apache-bullseye

RUN apt-get update && \
    apt-get install -y wget curl libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev vim-athena libonig-dev

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/
RUN docker-php-ext-install pdo_mysql mysqli gd iconv

# RUN echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
#     echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
#     echo "xdebug.client_port = 9003" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
#     echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
#     echo "xdebug.discover_client_host=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN apt-get install -y ssl-cert --no-install-recommends && \
    rm -r /var/lib/apt/lists/*

COPY php.ini /usr/local/etc/php/

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer