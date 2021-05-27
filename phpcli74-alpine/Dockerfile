FROM php:7.4-cli-alpine3.13

ENV PHPIZE_DEPS \
    autoconf \
    dpkg-dev dpkg \
    file \
    g++ \
    gcc \
    libc-dev \
    make \
    pkgconf \
    re2c

RUN set -eux; \
    apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    libzip-dev \
    zlib-dev \
    libpng-dev \
    jpeg-dev \
    imap-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    libldap \
    openldap-dev \
    krb5-dev \
    krb5 \
    libxml2-dev \
    icu-dev \
    postgresql-dev \
    imagemagick \
    imagemagick-libs \
    imagemagick-dev && \
    # ex
    docker-php-ext-configure gd \
    --with-freetype=/usr/include/ \
    --with-jpeg=/usr/include/ && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-configure ldap && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    docker-php-ext-install \
    soap \
    ldap \
    zip \
    bcmath \
    exif \
    gd \
    iconv \
    intl \
    pdo_mysql \
    pdo_pgsql \
    imap && \
    # ex
    printf "\npecl" | pecl install \
    redis \
    imagick \
    mongodb \
    && docker-php-ext-enable \
    imagick \
    mongodb \
    redis && \
    # clear pkg
    runDeps="$( \
    scanelf --needed --nobanner --format '%n#p' --recursive /usr/local \
    | tr ',' '\n' \
    | sort -u \
    | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )" && \
    apk add --no-cache $runDeps && \
    apk del --no-network .build-deps