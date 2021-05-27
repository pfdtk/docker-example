FROM php:7.4-cli

RUN apt-get update \
    && apt-get -y install \
    libc-client-dev \
    libkrb5-dev \
    imagemagick \
    libmagickwand-dev \
    libcurl3-dev \
    libicu-dev \
    libfreetype6-dev \
    libjpeg-dev \
    libpq-dev \
    libpng-dev \
    libxml2-dev \
    libzip-dev \
    libcurl4-openssl-dev \
    libonig-dev \
    libldap2-dev \
    --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN docker-php-ext-configure gd \
    --with-freetype=/usr/include/ \
    --with-jpeg=/usr/include/ && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-configure ldap && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install \
    soap \
    ldap \
    zip \
    curl \
    bcmath \
    exif \
    gd \
    iconv \
    intl \
    pdo_mysql \
    pdo_pgsql \
    imap \
    mbstring

RUN printf "\npecl" | pecl install \
    redis \
    imagick \
    mongodb \
    && docker-php-ext-enable \
    imagick \
    mongodb \
    redis