#####
# This image builds upon php-base
# Here we are going to 1) install and configure nginx and 2) install the init script, which will start and controll Nginx and PHP-FPM
# The result is an image upon which we can run PHP web applications
#####

ARG PHP_BASE_VERSION

#FROM gbmcarlos/php-base:${PHP_BASE_VERSION} as base

FROM 049836007356.dkr.ecr.eu-west-1.amazonaws.com/php-arm64:php-base as base


## System dependencies
#RUN amazon-linux-extras install \
        #nginx1.12

RUN apt-get update && apt-get install -y nginx

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
