FROM php:7.4-fpm
COPY php.ini /usr/local/etc/php/php.ini

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# Postgresql
RUN apt-get update \
    && apt-get -y install libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql pgsql

RUN apt-get update \
    && apt-get install -y --no-install-recommends libonig-dev libzip-dev git vim libpng-dev gnupg libnss3 libx11-dev wget openssh-client \
    && docker-php-ext-install zip gd \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Set composer environment
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# Laravel installer
# RUN composer global require "laravel/installer"

WORKDIR /var/www