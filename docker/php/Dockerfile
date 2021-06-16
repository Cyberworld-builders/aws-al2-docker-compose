FROM php:5.6.32-fpm

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

RUN docker-php-ext-install mysql mysqli
RUN apt-get update -y && apt-get install -y libpng-dev libmcrypt-dev

# may need to add back sendmail, it was somewhere in the above

RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev

RUN apt-get update && \
    apt-get install -y \
        libc-client-dev libkrb5-dev && \
    rm -r /var/lib/apt/lists/*

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install -j$(nproc) imap

RUN docker-php-ext-install zip
RUN docker-php-ext-install gd
RUN docker-php-ext-install exif

RUN docker-php-ext-install mcrypt

RUN docker-php-ext-configure hash --with-mhash

RUN apt-get update && apt-get install -y unixodbc-dev && rm -rf /var/lib/apt/lists/*
RUN docker-php-source extract \
    && set -x \
    && cd /usr/src/php/ext/odbc \
    && phpize \
    && sed -ri 's@^ *test +"\$PHP_.*" *= *"no" *&& *PHP_.*=yes *$@#&@g' configure \
    && docker-php-ext-configure odbc --with-unixODBC=shared,/usr \
    && docker-php-ext-install odbc \
    && docker-php-ext-enable odbc \
    && docker-php-source delete \
    && php -m

RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install sockets

RUN apt-get update && apt-get install -y libxml2-dev
RUN docker-php-ext-install wddx
RUN docker-php-ext-install xmlrpc

RUN docker-php-ext-install opcache

RUN apt-get install -y zlib1g-dev libicu-dev g++ \
&& docker-php-ext-configure intl \
&& docker-php-ext-install intl
