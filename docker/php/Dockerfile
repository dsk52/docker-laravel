FROM php:7.4.1-fpm-alpine

COPY php.ini /usr/local/etc/php/

RUN apk --no-cache --update add \
  autoconf \
  curl-dev \
  cmake \
  freetype-dev \
  libzip \
  libjpeg-turbo-dev \
  libpng-dev \
  libxml2 \
  libxml2-dev \
  zlib-dev \
  pcre-dev \
  g++ \
  make \
  openssl \
  gd \
  bash \
  vim \
  oniguruma \
  oniguruma-dev && \
  docker-php-ext-install \
  # ctype \ is already loaded!
  # json \ is already loaded!
  # mbstring \ is already loaded!
  # pdo \ is already loaded!
  # simplexml \ is already loaded!
  pdo_mysql \
  # zip \ peclからのインストールが必要みたい
  opcache \
  gd && \
  docker-php-ext-configure gd && \
  # --with-freetype-dir=/usr/include/ \
  # --with-jpeg-dir=/usr/include/ \
  # --with-png-dir=/usr/include/ && \
  apk --update --no-cache add tzdata && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  apk del tzdata && \
  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('sha384', 'composer-setup.php') === 'baf1608c33254d00611ac1705c1d9958c817a1a33bce370c0595974b342601bd80b92a3f46067da89e3b06bff421f182') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php && \
  php -r "unlink('composer-setup.php');"


RUN chown -R www-data:www-data /var/www
