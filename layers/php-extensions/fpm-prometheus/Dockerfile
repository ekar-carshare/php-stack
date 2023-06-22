ARG PHP_BASE_VERSION

#FROM gbmcarlos/php-base:${PHP_BASE_VERSION} as build
FROM 049836007356.dkr.ecr.eu-west-1.amazonaws.com/php-arm64:php-base as build

ARG TARGETARCH

RUN curl -L -O https://github.com/hipages/php-fpm_exporter/releases/download/v2.2.0/php-fpm_exporter_2.2.0_linux_$TARGETARCH.tar.gz \
    && tar -xf php-fpm_exporter_2.2.0_linux_$TARGETARCH.tar.gz \
    && mv php-fpm_exporter /opt/

FROM scratch as base

# Copy the binary
COPY --from=build --chmod=+x /opt/php-fpm_exporter /opt/bin/php-fpm_exporter