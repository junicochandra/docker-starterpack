ARG PHP_VERSION
FROM php:${PHP_VERSION}

#############################################
# System dependencies for Laravel
#############################################
RUN if grep -qi alpine /etc/os-release; then \
    apk add --no-cache \
        libzip-dev \
        libxml2-dev \
        oniguruma-dev \
        curl \
        unzip \
        freetype-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        postgresql-dev \
        $PHPIZE_DEPS \
    ; else \
    apt-get update && apt-get install -y \
        libzip-dev \
        libxml2-dev \
        libonig-dev \
        libpq-dev \
        zip \
        unzip \
        curl \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    ; fi

#############################################
# Configure GD extension with freetype and jpeg support
#############################################
RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg

#############################################
# PHP extensions
#############################################
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    mysqli \
    pdo_pgsql \
    pgsql \
    mbstring \
    bcmath \
    xml \
    zip \
    gd

#############################################
# Enable mysqli explicitly
#############################################
RUN docker-php-ext-enable mysqli

#############################################
# Composer
#############################################
USER root

ARG INSTALL_COMPOSER=false

RUN if [ "$INSTALL_COMPOSER" = "true" ]; then \
    curl -sS https://getcomposer.org/installer | php -- \
        --install-dir=/usr/local/bin \
        --filename=composer \
; fi
