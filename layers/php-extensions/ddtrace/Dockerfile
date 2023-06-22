#####
# This image builds upon php-base
# Download the source code of ddtrace, generate the ini file, and isolate them a clean image
#####

ARG DD_VERSION

ARG BASE_IMAGE_USER
ARG BASE_IMAGE_TAG
ARG BASE_IMAGE_ARCH

FROM ${BASE_IMAGE_USER}/php-base:${BASE_IMAGE_TAG}-${BASE_IMAGE_ARCH} as build

ARG DD_VERSION

RUN     curl -LOJ https://github.com/DataDog/dd-trace-php/releases/download/0.80.0/datadog-php-tracer_0.80.0_arm64.deb \
    &&  dpkg-deb -R datadog-php-tracer_0.80.0_arm64.deb extracted_contents \
    &&  mv extracted_contents/opt/* /opt/

RUN echo $'\
extension=/opt/datadog-php/extensions/no-debug-non-zts-20190902/ddtrace.so \n\
ddtrace.request_init_hook=/opt/datadog-php/dd-trace-sources/bridge/dd_wrap_autoloader.php' \
    > /tmp/ext.ini

FROM scratch as base

# Copy the extensions, the source for the tracer and the statsd, and the ini file
COPY --from=build /opt/datadog-php/extensions/ddtrace-20190902.so /opt/datadog-php/extensions/no-debug-non-zts-20190902/ddtrace.so
COPY --from=build /opt/datadog-php/dd-trace-sources /opt/datadog-php/dd-trace-sources
COPY --from=build /tmp/ext.ini /opt/bref/etc/php/conf.d/ext-ddtrace.ini