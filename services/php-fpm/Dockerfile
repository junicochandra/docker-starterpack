ARG PHP_VERSION
FROM php:${PHP_VERSION}

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable mysqli


###########################################################################
# composer:
###########################################################################
USER root

ARG INSTALL_COMPOSER=false
RUN if [ ${INSTALL_COMPOSER} = true ]; then \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  ;fi
