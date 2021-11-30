ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:10.2.3
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Copy root filesystem
COPY rootfs /

# Setup base
RUN apk add --no-cache \
	build-base \
	argp-standalone \
	autoconf \
	automake \
	gcc \
	make \
	git

#RUN apk add --no-cache mosquitto-dev


WORKDIR /build
RUN git clone https://github.com/john30/ebusd.git /build
RUN ./autogen.sh && make && make install


RUN ./src/ebusd/ebusd --help
#RUN ./src/ebusd/ebusd --usage


# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Dennis Koot <koter84@gmail.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="koter84" \
    org.opencontainers.image.authors="Dennis Koot <koter84@gmail.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/koter84/addon-ebusd" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
