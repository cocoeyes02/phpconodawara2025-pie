FROM php:8.4-fpm
SHELL ["/bin/bash", "-c"]

COPY ./php.ini /usr/local/etc/php/php.ini

RUN apt-get update && \
    apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
    docker-php-ext-install zip intl mbstring
RUN pecl install xdebug-3.4.2
RUN docker-php-ext-enable xdebug

RUN touch /tmp/xdebug.log && chmod 666 /tmp/xdebug.log

WORKDIR /var/www/html