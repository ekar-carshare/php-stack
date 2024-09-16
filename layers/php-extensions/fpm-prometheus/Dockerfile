ARG BASE_IMAGE_USER
ARG BASE_IMAGE_TAG
ARG BASE_IMAGE_ARCH

FROM ${BASE_IMAGE_USER}/php-base:${BASE_IMAGE_TAG}-${BASE_IMAGE_ARCH} as build

ARG BASE_IMAGE_ARCH

RUN     curl -L -O https://github.com/hipages/php-fpm_exporter/releases/download/v2.2.0/php-fpm_exporter_2.2.0_linux_$BASE_IMAGE_ARCH.tar.gz \
    &&  tar -xf php-fpm_exporter_2.2.0_linux_$BASE_IMAGE_ARCH.tar.gz \
    &&  mv php-fpm_exporter /opt/

FROM scratch as base

# Copy the binary
COPY --from=build --chmod=+x /opt/php-fpm_exporter /opt/bin/php-fpm_exporter