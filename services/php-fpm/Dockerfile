ARG PHP_VERSION
FROM php:${PHP_VERSION}

#############################################
# [NEW] system dependencies for Laravel
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
    ; else \
    apt-get update && apt-get install -y \
        libzip-dev \
        libxml2-dev \
        libonig-dev \
        zip \
        unzip \
        curl \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        && rm -rf /var/lib/apt/lists/* \
    ; fi

#############################################
# [CHANGED] Laravel required PHP extensions
#############################################
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    mysqli \
    mbstring \
    bcmath \
    xml \
    zip \ 
    gd

#############################################
# [UNCHANGED] enable mysqli explicitly
#############################################
RUN docker-php-ext-enable mysqli

#############################################
# composer
#############################################
USER root

ARG INSTALL_COMPOSER=false

# [CHANGED] safer condition check
RUN if [ "$INSTALL_COMPOSER" = "true" ]; then \
    curl -sS https://getcomposer.org/installer | php -- \
        --install-dir=/usr/local/bin \
        --filename=composer \
; fi
