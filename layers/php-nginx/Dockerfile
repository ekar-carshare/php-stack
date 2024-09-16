#####
# This image builds upon php-base
# Here we are going to 1) install and configure nginx and 2) install the init script, which will start and controll Nginx and PHP-FPM
# The result is an image upon which we can run PHP web applications
#####

ARG BASE_IMAGE_USER
ARG BASE_IMAGE_TAG
ARG BASE_IMAGE_ARCH

FROM ${BASE_IMAGE_USER}/php-base:${BASE_IMAGE_TAG}-${BASE_IMAGE_ARCH} as base

RUN     apt-get update \
    &&  apt-get install -y nginx

### Set up permissions
RUN groupadd www \
    && useradd -g www www \
    && mkdir -p /var/tmp/nginx \
    && chown -R www:www /var/tmp/nginx \
    && chown -R www:www /tmp

### Copy the init script
COPY init.sh /opt/bin/init.sh

### By default, execute the init.sh script
CMD ["/bin/sh", "-c", "/opt/bin/init.sh"]

WORKDIR /var/task
