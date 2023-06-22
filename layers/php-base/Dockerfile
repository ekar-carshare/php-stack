#####
# This image builds upon Bref's compiled php
# Here we are going to fix a few things and replace a few others
# The result is an image where /opt contains everything required to execute PHP (+php-fpm, +composer)
#####

ARG COMPOSER_VERSION
ARG PHP_VERSION
ARG PHP_VERSION_SHORT
ARG BREF_VERSION

## Composer
### We extract composer executable from this image
#FROM composer:${COMPOSER_VERSION} as target-composer
FROM composer:2.0 as target-composer

## PHP config
### We extract php's production-ready config file from this image
FROM php:7.4 as target-php

#FROM bref/php-${PHP_VERSION_SHORT}-fpm:${BREF_VERSION} as base
FROM php:7.4-fpm-buster as base

### We need to switch to root to use yum
USER root

### According to https://forums.aws.amazon.com/thread.jspa?messageID=755409&tstart=0, we need to install yum-plugin-ovl to avoid errors like "Rpmdb checksum is invalid"
### vim, htop, less and tree are utilities to work inside the container more comfortably
### git, zip and unzip are necessary for Composer to install dependencies

# RUN     yum install -y \
#             amazon-linux-extras \
#             yum-plugin-ovl \
#             vim htop less tree \
#             git zip unzip tar

RUN apt-get update && apt-get install -y \
    vim htop less tree git zip unzip tar


### Replace bref's config file with the oficial PHP image's config file
#RUN rm /opt/bref/etc/php/conf.d/bref.ini
#COPY --from=target-php /usr/local/etc/php/php.ini-production /opt/bref/etc/php/conf.d/php.ini

COPY --from=target-php "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

### Add composer
COPY --from=target-composer /usr/bin/composer /usr/bin/composer

### Add /usr/sbin to the path
ENV PATH="/usr/sbin:${PATH}"