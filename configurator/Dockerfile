ARG BUILD_FROM
FROM $BUILD_FROM

ENV PIP_BREAK_SYSTEM_PACKAGES=1

# Setup base
ARG BUILD_ARCH
ARG CONFIGURATOR_VERSION
RUN \
    apk add --no-cache \
        git \
        openssh-client \
        py3-pip \
        python3 \
    && pip3 install --no-cache-dir git+https://github.com/hector-romero/hass-configurator.git@mobile-fixes \
    \
    && find /usr/local \
        \( -type d -a -name test -o -name tests -o -name '__pycache__' \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' +

# Copy data
COPY rootfs /

# Health check
HEALTHCHECK CMD curl --fail http://127.0.0.1:8099 || exit 1
