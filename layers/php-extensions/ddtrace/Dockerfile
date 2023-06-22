#####
# This image builds upon php-base
# Download the source code of ddtrace, generate the ini file, and isolate them a clean image
#####

ARG DD_VERSION

ARG PHP_VERSION_SHORT
ARG BREF_VERSION

#FROM bref/build-php-${PHP_VERSION_SHORT}:${BREF_VERSION} as build

FROM 049836007356.dkr.ecr.eu-west-1.amazonaws.com/php-arm64:php-base as build

ARG DD_VERSION


# RUN     curl -sL https://github.com/DataDog/dd-trace-php/releases/download/${DD_VERSION}/datadog-php-tracer-${DD_VERSION}.x86_64.tar.gz | tar -xz \
#     &&  mv opt/* /opt/

RUN     curl -LOJ https://github.com/DataDog/dd-trace-php/releases/download/0.80.0/datadog-php-tracer_0.80.0_arm64.deb \
        && dpkg-deb -R datadog-php-tracer_0.80.0_arm64.deb extracted_contents \
        &&  mv extracted_contents/opt/* /opt/

RUN echo $'\
extension=/opt/datadog-php/extensions/no-debug-non-zts-20190902/ddtrace.so \n\
ddtrace.request_init_hook=/opt/datadog-php/dd-trace-sources/bridge/dd_wrap_autoloader.php' \
    > /tmp/ext.ini


#ENTRYPOINT ["php-fpm"]

FROM scratch as base

# Copy the extensions, the source for the tracer and the statsd, and the ini file
COPY --from=build /opt/datadog-php/extensions/ddtrace-20190902.so /opt/datadog-php/extensions/no-debug-non-zts-20190902/ddtrace.so
COPY --from=build /opt/datadog-php/dd-trace-sources /opt/datadog-php/dd-trace-sources
COPY --from=build /tmp/ext.ini /opt/bref/etc/php/conf.d/ext-ddtrace.ini