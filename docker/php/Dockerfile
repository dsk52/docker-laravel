FROM php:7.4.1-fpm-alpine

COPY php.ini /usr/local/etc/php/

RUN apk --no-cache --update add \
  autoconf \
  curl-dev \
  cmake \
  libzip \
  libpng-dev \
  libxml2 \
  libxml2-dev \
  zlib-dev \
  pcre-dev \
  g++ \
  make \
  gd \
  bash \
  vim \
  icu-dev \
  libzip-dev \
  oniguruma-dev && \
  docker-php-ext-install \
  intl \
  mbstring \
  bcmath \
  pdo_mysql \
  zip \
  opcache \
  gd && \
  docker-php-ext-configure \
  zip && \
  # opcache \
   # pdo_mysql \
  # sodium \
  apk --update --no-cache add tzdata && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  apk del tzdata && \
  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('sha384', 'composer-setup.php') === 'baf1608c33254d00611ac1705c1d9958c817a1a33bce370c0595974b342601bd80b92a3f46067da89e3b06bff421f182') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php && \
  php -r "unlink('composer-setup.php');" && \
  mv composer.phar /usr/local/bin/composer && \
  composer global require laravel/installer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www

RUN chown -R www-data:www-data /var/www
