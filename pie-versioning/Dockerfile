FROM php:8.4-fpm
SHELL ["/bin/bash", "-c"]

COPY ./php.ini /usr/local/etc/php/php.ini

RUN export DEBIAN_FRONTEND="noninteractive" &&  \
    set -eux && \
    apt-get update && \
    apt-get install -y --no-install-recommends autoconf automake libtool m4 make gcc git unzip libzip-dev libicu-dev libonig-dev && \
    rm -rf /var/lib/apt/lists/*

RUN curl -L --output /usr/local/bin/pie https://github.com/php/pie/releases/latest/download/pie.phar && chmod +x /usr/local/bin/pie
COPY --from=ghcr.io/php/pie:bin /pie /usr/bin/pie

RUN docker-php-ext-install zip intl mbstring
RUN pie install xdebug/xdebug:3.4.1||3.4.0
RUN docker-php-ext-enable xdebug
RUN touch /tmp/xdebug.log && chmod 666 /tmp/xdebug.log

WORKDIR /var/www/html