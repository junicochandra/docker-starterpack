ARG PHP_VERSION
FROM php:${PHP_VERSION}

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable mysqli
 

###########################################################################
# symfony5 installer:
###########################################################################
USER root

ARG INSTALL_SYMFONY5=false
RUN if [ ${INSTALL_SYMFONY5} = true ]; then \
  curl -sS https://get.symfony.com/cli/installer | bash \
  ;fi

RUN if [ ${INSTALL_SYMFONY5} = true ]; then \
  mv /root/.symfony5/bin/symfony /usr/local/bin/symfony \
  ;fi

###########################################################################
# composer:
###########################################################################
USER root

ARG INSTALL_COMPOSER=false
RUN if [ ${INSTALL_COMPOSER} = true ]; then \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  ;fi

###########################################################################
# Human Language and Character Encoding Support:
###########################################################################

ARG INSTALL_INTL=false

RUN if [ ${INSTALL_INTL} = true ]; then \
  apt-get -y update \
  && apt-get install -y libicu-dev \ 
  && docker-php-ext-configure intl \
  && docker-php-ext-install intl \
  ;fi

WORKDIR /var/www