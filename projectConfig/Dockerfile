FROM php:7.1.3-apache

MAINTAINER Morten Hartvig <hartvigmorten@gmail.com>

# Avoid questions during installation
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get install -y libmcrypt-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libfreetype6-dev \
        libxml2-dev \
        libicu-dev \
        wget \
        unzip \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install \
        iconv \
        intl \
        mcrypt \
        opcache \
        pdo \
        mysqli \
        pdo_mysql \
        mbstring \
        soap \
        gd \
        zip \
        pcntl 

# Install Xdebug
RUN curl -fsSL 'https://xdebug.org/files/xdebug-2.5.1.tgz' -o xdebug.tar.gz \
    && mkdir -p xdebug \
    && tar -xf xdebug.tar.gz -C xdebug --strip-components=1 \
    && rm xdebug.tar.gz \
    && ( \
    	cd xdebug \
    	&& phpize \
    	&& ./configure --enable-xdebug \
    	&& make -j$(nproc) \
    	&& make install \
    ) \
    && rm -r xdebug \
    && docker-php-ext-enable xdebug

# Apache configuration
RUN a2enmod rewrite

# PHP configuration
COPY php.ini /usr/local/etc/php/

VOLUME /var/www/html/
WORKDIR /var/www/html/
EXPOSE 80
CMD ["apache2-foreground"]
