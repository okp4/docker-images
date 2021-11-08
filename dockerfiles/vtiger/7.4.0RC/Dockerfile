FROM php:7.0-apache

RUN apt-get update -y 
RUN apt-get install -y git

RUN a2enmod rewrite expires

# install the PHP extensions we need
RUN apt-get install -y cron curl wget libpng-dev libjpeg-dev libkrb5-dev zlib1g-dev \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd mysqli \
    && apt-get -y install libssl-dev libc-client2007e-dev libkrb5-dev \
    && docker-php-ext-configure imap --with-imap-ssl --with-kerberos \
    && docker-php-ext-install imap opcache zip\
&& rm -rf /var/lib/apt/lists/*

RUN chown -R www-data:www-data /var/www/html

# vtiger server
RUN git clone --depth 1 --branch 7.4.0RC https://code.vtiger.com/vtiger/vtigercrm.git /var/www/html
