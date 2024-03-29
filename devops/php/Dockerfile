FROM php:8.1-fpm

RUN apt-get update && apt-get install -y zlib1g-dev libicu-dev zip libzip-dev libpq-dev zip vim \
    && docker-php-ext-install intl opcache pdo pdo_pgsql pgsql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql

COPY php.ini /usr/local/etc/php/conf.d/
COPY lite_php_browscap.ini /usr/local/etc/php/conf.d/

RUN pecl install xdebug-3.1.1 \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.mode = debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host=10.254.254.254" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_port=9003" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.discover_client_host=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey=phpstorm" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "browscap=/usr/local/etc/php/conf.d/lite_php_browscap.ini" >> /usr/local/etc/php/conf.d/docker-php-ext-browscap.ini

WORKDIR /var/www/url-shorter
