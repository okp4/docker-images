FROM php:7.0-apache

RUN a2enmod rewrite expires

# install the PHP extensions we need
RUN apt-get --no-install-recommends update && apt-get --no-install-recommends install -y git=1:2.11.0-3+deb9u7 \
    cron=3.0pl1-128+deb9u2 curl=7.52.1-5+deb9u16 wget=1.18-5+deb9u3 libpng-dev=1.6.28-1+deb9u1 libjpeg-dev=1:1.5.1-2+deb9u1 libkrb5-dev=1.15-1+deb9u3 zlib1g-dev=1:1.2.8.dfsg-5 \
    libssl-dev=1.1.0l-1~deb9u4 libc-client2007e-dev=8:2007f~dfsg-5 libkrb5-dev=1.15-1+deb9u3 \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd mysqli \
    && docker-php-ext-configure imap --with-imap-ssl --with-kerberos \
    && docker-php-ext-install imap opcache zip \
    && rm -rf /var/lib/apt/lists/* \
    && git clone --depth 1 --branch 7.2.0 https://code.vtiger.com/vtiger/vtigercrm.git /var/www/html \
    && chown -R www-data:www-data /var/www/html \
    && rm -rf /var/www/html/.git \
    && apt-get -y remove git
