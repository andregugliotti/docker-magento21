FROM php:5.6-fpm

RUN useradd -u 1000 local -d "/home/local"

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        apt-utils \
        libxml2-dev \
        zlib1g-dev \
        zip \
        php-http \
        php5-dev \
        libcurl3 \
        libpcre3-dev \
        libcurl4-openssl-dev \
        libicu-dev \
        libxml2-dev libxslt-dev \
        zlib1g-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt pdo_mysql mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install soap

RUN apt-get install -y git

RUN docker-php-ext-configure bcmath \
    && docker-php-ext-install -j$(nproc) bcmath

RUN docker-php-ext-configure intl \
    && docker-php-ext-install intl

RUN docker-php-ext-configure xsl \
    && docker-php-ext-install xsl

RUN docker-php-ext-configure zip \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

COPY xdebug-2.5.4.tgz /usr/src/php/ext/xdebug.tgz
RUN tar -xf /usr/src/php/ext/xdebug.tgz -C /usr/src/php/ext/ && \
    rm /usr/src/php/ext/xdebug.tgz && \
    docker-php-ext-install xdebug-2.5.4
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

COPY magento.ini /usr/local/etc/php/conf.d/90-magento.ini
# to include ioncube support, uncomment the next two lines
#COPY ioncube/ioncube_loader_lin_5.6.so /usr/lib/php5/20131226/ioncube_loader_lin_5.6.so
#COPY ioncube.ini /usr/local/etc/php/php.ini