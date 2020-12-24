FROM php:8.0-fpm-alpine

RUN apk --update add \
    autoconf \
    build-base \
    linux-headers \
    libaio-dev \
    zlib-dev \
    curl \
    git \
    subversion \
    freetype-dev \
    libjpeg-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libtool \
    libbz2 \
    bzip2 \
    bzip2-dev \
    libstdc++ \
    libxslt-dev \
    openldap-dev \
#    imagemagick-dev \
    libzip-dev \
    oniguruma-dev \
    make \
    unzip \
    wget && \
    docker-php-ext-install bcmath zip bz2 pdo_mysql mysqli simplexml opcache sockets mbstring pcntl xsl && \
    docker-php-ext-configure gd && \
#    pecl install imagick && \
#    docker-php-ext-enable imagick && \
    pecl install swoole && \
    docker-php-ext-enable swoole && \
    docker-php-ext-install gd && \
    docker-php-ext-enable opcache && \
    apk del build-base \
    linux-headers \
    libaio-dev \
    && rm -rf /var/cache/apk/*

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp
ENV COMPOSER_VERSION 1.5.1

RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

VOLUME /var/www/html
WORKDIR /var/www/html

CMD php-fpm