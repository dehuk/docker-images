FROM php:5.6.30-apache

# PHP Core Extensions
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libssl-dev \
    && docker-php-ext-install iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# Extensions bcmath
RUN docker-php-ext-configure bcmath \
    && docker-php-ext-install bcmath

# Extensions bz2
RUN apt-get update \
    && apt-get install -y libbz2-dev \
    && docker-php-ext-configure bz2 \
    && docker-php-ext-install bz2

# Extensions calendar
RUN docker-php-ext-configure calendar \
    && docker-php-ext-install calendar

# Extensions curl
RUN apt-get update \
    && apt install -y curl libcurl3 libcurl3-dev \
    && docker-php-ext-configure curl \
    && docker-php-ext-install curl

# Extensions exif
RUN docker-php-ext-configure exif \
    && docker-php-ext-install exif

# Extensions gettex
RUN docker-php-ext-configure gettext \
    && docker-php-ext-install gettext

# Extensions gmp
RUN apt-get update \
    && apt-get install -y libgmp-dev \
    && ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h \
    && docker-php-ext-configure gmp \
    && docker-php-ext-install gmp

# Extensions hash
RUN docker-php-ext-configure hash --with-mhash  \
    && docker-php-ext-install hash

# Extensions imap
RUN apt-get update \
    && apt-get install -y libc-client-dev libkrb5-dev \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap

# Extensions intl
RUN apt-get update \
    && apt-get install -y --no-install-recommends libicu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl

# Extensions ldap
RUN apt-get update \
    && apt install -y libldap2-dev \
    && ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu \
    && docker-php-ext-install ldap

# Extensions mbstring
RUN docker-php-ext-configure mbstring \
    && docker-php-ext-install mbstring

# Extensions mysqli
RUN docker-php-ext-configure mysqli --with-mysqli=mysqlnd \
    && docker-php-ext-install mysqli

# Extensions pcntl
RUN docker-php-ext-configure pcntl \
    && docker-php-ext-install pcntl

# Extensions pdo
RUN docker-php-ext-configure pdo \
    && docker-php-ext-install pdo

# Extensions pdo_mysql
RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-install pdo_mysql

# Extensions pspell
RUN apt-get update \
    && apt install -y libpspell-dev \
    && docker-php-ext-configure pspell \
    && docker-php-ext-install pspell

# Extensions shmop
RUN docker-php-ext-configure shmop \
    && docker-php-ext-install shmop

# Extensions sockets
RUN docker-php-ext-configure sockets \
    && docker-php-ext-install sockets

# Extensions sysvmsg
RUN docker-php-ext-configure sysvmsg \
    && docker-php-ext-install sysvmsg

# Extensions sysvsem
RUN docker-php-ext-configure sysvsem \
    && docker-php-ext-install sysvsem

# Extensions sysvshm
RUN docker-php-ext-configure sysvshm \
    && docker-php-ext-install sysvshm

# Extensions wddx
RUN docker-php-ext-configure wddx --enable-libxml \
    && docker-php-ext-install wddx

# Extensions xml
RUN apt-get update \
    && apt-get install -y --no-install-recommends libxml2-dev libxslt1-dev \
    && docker-php-ext-configure xml \
    && docker-php-ext-install xml

# Extensions xsl
RUN apt-get update \
    && apt-get install -y --no-install-recommends libxslt-dev \
    && docker-php-ext-configure xsl \
    && docker-php-ext-install xsl

# Extensions zip
RUN apt-get update \
    && apt-get install -y --no-install-recommends zlib1g-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-install zip

RUN a2enmod rewrite

COPY config/apache/000-default.conf /etc/apache2/sites-available/000-default.conf

COPY config/php/php.ini $PHP_INI_DIR/conf.d/memory-limit.ini

# Install utils
RUN apt-get update \
    && apt-get install -y nano git mysql-client wget\
    && rm -r /var/lib/apt/lists/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

# Other settings
VOLUME /var/www/html

WORKDIR /var/www/html