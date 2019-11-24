FROM php:7.3-cli

RUN apt-get update && apt-get install -y libc-client-dev libkrb5-dev && apt-get clean
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap \
    && docker-php-ext-enable imap