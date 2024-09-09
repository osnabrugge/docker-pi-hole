# Use Debian 12 as the base image
FROM debian:12

# Set build arguments
ARG DEBIAN_VERSION=debian-12
ARG PIHOLE_DOCKER_TAG=2024.07.0

# Set environment variables
ENV phpver=php

# Install required packages
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    lighttpd \
    php-common \
    php-cgi \
    php-sqlite3 \
    php-xml \
    php-intl \
    php-json \
    dnsutils \
    idn2 \
    dns-root-data \
    ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Handle specific Debian version logic
RUN if [ "$DEBIAN_VERSION" = "buster-slim" ]; then c_rehash; fi

# Set Pi-hole Docker tag
RUN echo "${PIHOLE_DOCKER_TAG}" > /pihole.docker.tag

# Set the entrypoint
ENTRYPOINT ["/usr/local/bin/s6-init"]

# Copy additional files
COPY s6/debian-root/etc /etc
COPY s6/debian-root/usr /usr