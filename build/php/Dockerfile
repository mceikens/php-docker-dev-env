FROM php:7.3-fpm

USER root

RUN apt-get update
RUN apt-get install -y \
    build-essential \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libzip-dev \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    curl \
    python \
    git \
    libxml2-dev \
    zlib1g-dev \
    libbz2-dev \
    libcurl4-openssl-dev \
    libxslt-dev \
    libsqlite3-dev \
    graphicsmagick \
    locales-all \
    libgmp-dev \
    make \
    gcc \
    autoconf \
    ghostscript \
    nfs-common \
    libc-dev \
    pkg-config \
    libgd3 \
    libgd-dev \
    libssl-dev

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-gd --with-webp-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-xpm-dir --with-freetype-dir
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install iconv \
                          intl \
                          mbstring \
                          opcache \
                          pdo \
                          soap \
                          xml \
                          bz2 \
                          curl \
                          fileinfo\
                          ftp \
                          gettext \
                          simplexml \
                          tokenizer \
                          xsl \
                          pdo_mysql \
                          pdo_sqlite \
                          mysqli \
                          bcmath \
                          gmp \
                          zip

RUN pecl install apcu
RUN docker-php-ext-enable apcu

RUN pecl install redis
RUN docker-php-ext-enable redis

RUN yes | pecl xdebug \
    && echo "zed_extension=$(find $(php-config --extension-dir) -name xdebug.so)" \
        > /usr/local/etc/php/conf.d/xdebug.ini

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

RUN chown -R www.www /var/www
RUN chmod -R 755 /var/www

COPY /build/php/conf/php.ini /usr/local/etc/php

WORKDIR /var/www
COPY . $PROJECT_VOLUMES

USER www

EXPOSE 9000
CMD ["php-fpm"]
