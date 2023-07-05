ARG COMPOSER_VERSION=2.0
ARG PHP_VERSION=7.4

## Composer
### We extract composer executable from this image
FROM composer:${COMPOSER_VERSION} as target-composer

FROM php:${PHP_VERSION}-fpm-buster as base

WORKDIR /var/task

RUN     apt-get update \
    &&  apt-get install -y \
            vim htop less tree git zip unzip tar \
            libxml2-dev

RUN     docker-php-ext-install pcntl soap pdo pdo_mysql \
    &&  docker-php-ext-enable pcntl soap

### Add composer
COPY --from=target-composer /usr/bin/composer /opt/bin/composer

### Add /usr/sbin to the path
ENV PATH="/opt/bin:/usr/sbin:${PATH}"