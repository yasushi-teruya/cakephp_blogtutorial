FROM php:7.3-apache

RUN apt-get upgrade && apt-get update && apt-get install -y \
  vim \
  openssl \
  libssl-dev \
  ssl-cert \
  libicu-dev \
  unzip \
  libxml2 \
  libxml2-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && a2enmod ssl \
  && a2ensite default-ssl \
  && docker-php-ext-install intl \
  && docker-php-ext-install pdo_mysql \
  && docker-php-ext-install mysqli \
  && docker-php-ext-install mbstring \
  && docker-php-ext-install simplexml

RUN /bin/bash -c a2enmod rewrite

COPY ./cert/cert-key.pem /usr/local/apache2/cert/
COPY ./cert/cert.pem /usr/local/apache2/cert/

COPY ./conf/httpd.conf /etc/apache2/apache2.conf
COPY ./conf/ssl.conf /etc/apache2/sites-available/ssl.conf

COPY ./php/php.ini /usr/local/etc/php/php.ini
