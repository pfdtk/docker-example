FROM php:7.3-fpm

RUN apt-get update \
    && apt-get -y install \
        apt-utils \
        libc-client-dev \
        libkrb5-dev \
        g++ \
        git \
        curl \
        imagemagick \
        libcurl3-dev \
        libicu-dev \
        libfreetype6-dev \
        libjpeg-dev \
        libjpeg62-turbo-dev \
        libmagickwand-dev \
        libpq-dev \
        libpng-dev \
        libxml2-dev \
        libzip-dev \
        zlib1g-dev \
        default-mysql-client \
        openssh-client \
        nano \
        unzip \
        libcurl4-openssl-dev \
        libssl-dev \
        --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install \
        soap \
        zip \
        curl \
        bcmath \
        exif \
        gd \
        iconv \
        intl \
        mbstring \
        opcache \
        pdo_mysql \
        pdo_pgsql \
        imap

RUN printf "\npecl" | pecl install \
    imagick \
    mongodb \
    && docker-php-ext-enable \
        imagick \
        mongodb