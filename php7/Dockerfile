FROM php:7-apache

RUN apt-get update \
    && apt-get install -y wget libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev vim-athena
RUN docker-php-ext-install pdo_mysql mysqli mbstring gd iconv

RUN pecl install xdebug mcrypt-1.0.1 && \
    docker-php-ext-enable xdebug mcrypt

RUN echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN a2enmod rewrite

RUN apt-get install -y ssl-cert \
  --no-install-recommends && rm -r /var/lib/apt/lists/*

COPY php.ini /usr/local/etc/php/

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

RUN wget https://phar.phpunit.de/phpunit-6.5.phar && \
    chmod +x phpunit-6.5.phar && \
    mv phpunit-6.5.phar /usr/local/bin/phpunit && \
    phpunit --version