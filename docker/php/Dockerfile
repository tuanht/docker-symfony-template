FROM php:8.0-fpm-alpine

LABEL maintainer="Tuan Ha <tuanht.unix@gmail.com>"

RUN apk upgrade -U && \
  apk --update add \
  freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev icu-dev \
  coreutils git bash \
  gd mysql-client \
  libgcc libstdc++ glib \
  $PHPIZE_DEPS

# Get source & config
ADD https://pecl.php.net/get/apcu-5.1.21.tgz /tmp/apcu.tar.gz
RUN mkdir -p /usr/src/php/ext/apcu\
  && tar xf /tmp/apcu.tar.gz -C /usr/src/php/ext/apcu --strip-components=1

RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/5.3.4.tar.gz \
  && tar xfz /tmp/redis.tar.gz \
  && rm -r /tmp/redis.tar.gz \
  && mv phpredis-5.3.4 /usr/src/php/ext/redis

# Install php extensions
RUN docker-php-ext-configure apcu
# RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install apcu pdo_mysql opcache bcmath redis zip intl gd
RUN docker-php-ext-install -j$(nproc) gd

# Install Xdebug
RUN pecl install xdebug \
  && docker-php-ext-enable xdebug
COPY xdebug.ini /tmp
RUN cat /tmp/xdebug.ini >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
  && rm /tmp/xdebug.ini

COPY php.ini /usr/local/etc/php/conf.d

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www
