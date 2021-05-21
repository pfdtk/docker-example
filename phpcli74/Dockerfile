FROM php:7.4-cli


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
    --with-freetype=/usr/include/ \
    --with-jpeg=/usr/include/ && \
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
    pdo_mysql \
    pdo_pgsql \
    imap

RUN apt-get update && apt-get -y install libonig-dev

RUN docker-php-ext-install mbstring

RUN printf "\npecl" | pecl install \
    imagick \
    mongodb \
    && docker-php-ext-enable \
    imagick \
    mongodb

RUN printf "\npecl" | pecl install redis \
    && docker-php-ext-enable \
    redis

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py --user;

ENV PATH="~/.local/bin:$PATH"

RUN /root/.local/bin/pip3 install awscli --upgrade --user

RUN apt-get -y install ffmpeg

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

COPY php.ini $PHP_INI_DIR