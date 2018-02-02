FROM php:5.6-apache

RUN apt-get update && apt-get install -y \
        vim \
        git \
        zip \
        unzip \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) \
        iconv \
        mbstring \
        pdo_mysql \
        mysqli \
        mcrypt

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN a2enmod rewrite

COPY ./vhost.conf /etc/apache2/sites-enable/
COPY ./php.ini /usr/local/etc/php/

RUN echo "postfix postfix/main_mailer_type string Internet site" > preseed.txt \
    && echo "postfix postfix/mailname string mail.example.com" >> preseed.txt \
    && debconf-set-selections preseed.txt \
    && DEBIAN_FRONTEND=noninteractive apt-get install -q -y postfix \
    && postfix start