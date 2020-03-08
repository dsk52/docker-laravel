FROM php:7.3.15-fpm-alpine

# イメージアップデート&タイムゾーン設定
RUN apk update && \
  apk --update --no-cache add \
  tzdata && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  apk del tzdata && \

# 必要パッケージのインストール
RUN chown -R www-data:www-data /var/www && \
  apk --update --no-cache add \
  apk --no-cache add \
  autoconf \
  bzip2-dev \
  gcc \
  g++ \
  make \
  libzip \
  libpng-dev \
  libxml2 \
  libxml2-dev \
  libxslt \
  libxslt-dev \
  zlib-dev \
  libzip-dev \
  oniguruma-dev \
  libmemcached-dev && \
  # PHPの拡張パッケージのインストール
  docker-php-ext-install \
    bcmath \
    # ctype \ # already installed
    # json \ # already installed
    # mbstring \ # already installed
    # openssl \ # already installed
    # pdo \ # already installed
    # tokenizer \ # already installed
    # xml \ # already installed
    gd \
    opcache \
    xmlrpc \
    zip \
    bz2 \
    calendar \
    pcntl \
    pdo_mysql \
    xsl \
    wddx && \
  docker-php-ext-configure \
    zip && \
  pecl install \
    igbinary \
    msgpack \
    memcached && \
  docker-php-ext-enable \
    igbinary \
    msgpack \
    memcached && \
  apk del g++ make cmake

# composer 1.9.3
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('sha384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php && \
  php -r "unlink('composer-setup.php');" && \
  mv composer.phar /usr/local/bin/composer && \
  # laravelインストーラーのインストール
  composer global require laravel/installer && \
  # 不要パッケージ削除

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www
