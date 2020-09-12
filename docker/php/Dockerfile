FROM php:7.3.22-fpm-alpine

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
  zip
  # opcache \
   # pdo_mysql \
  # sodium \

RUN apk --update --no-cache add tzdata && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  apk del tzdata

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('sha384', 'composer-setup.php') === '795f976fe0ebd8b75f26a6dd68f78fd3453ce79f32ecb33e7fd087d39bfeb978342fb73ac986cd4f54edd0dc902601dc') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php && \
  php -r "unlink('composer-setup.php');" && \
  mv composer.phar /usr/local/bin/composer && \
  composer global require laravel/installer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www

RUN chown -R www-data:www-data /var/www
