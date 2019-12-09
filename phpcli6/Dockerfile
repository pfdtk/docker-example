FROM php:5.6-cli

#RUN echo "deb https://mirrors.tuna.tsinghua.edu.cn/debian buster main\ndeb https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main\ndeb https://mirrors.tuna.tsinghua.edu.cn/debian buster-updates main" > /etc/apt/sources.list 


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

RUN apt update && apt-get -y install openssh-server && \
    mkdir /var/run/sshd && \
    mkdir -p ~/.ssh \
    && echo 'root:111111' | chpasswd \
    && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

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
        pdo_mysql \
        pdo_pgsql \
        imap

RUN printf "\npecl" | pecl install \
    imagick \
    mongodb \
    && docker-php-ext-enable \
        imagick \
        mongodb

# use with build.args in docker-compos.yml
# ARG SSH_KEY_PATH

RUN docker-php-ext-configure mysql && \
    docker-php-ext-configure mysqli && \
    docker-php-ext-install \
        mysql \
        mysqli

RUN printf "\npecl" | pecl install redis-3.1.0 \
    && docker-php-ext-enable \
        redis

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py --user;

ENV PATH="~/.local/bin:$PATH"

RUN /root/.local/bin/pip3 install awscli --upgrade --user

RUN apt-get update && \
    apt-get install libldap2-dev -y && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install \
        ldap

RUN printf "\npecl" | pecl install \
    mongo \
    && docker-php-ext-enable \
        mongo

RUN printf "\npecl" | pecl install \
    igbinary-2.0.5 \
    && docker-php-ext-enable \
        igbinary


COPY php.ini $PHP_INI_DIR

RUN curl -O https://johnvansickle.com/ffmpeg/releases/ffmpeg-release-amd64-static.tar.xz && \
    tar xf ffmpeg-release-amd64-static.tar.xz && \
    mv ffmpeg-4.2.1-amd64-static /usr/local/ffmpeg