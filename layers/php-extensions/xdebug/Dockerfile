FROM php:7.4-fpm-buster as build

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN install-php-extensions xdebug-3.0.3

FROM scratch as base

COPY --from=build /usr/local/lib/php/extensions/no-debug-non-zts-20190902/xdebug.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/xdebug.so
COPY --from=build /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini