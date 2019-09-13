FROM php:7.1-fpm

RUN docker-php-ext-install mysqli pdo pdo_mysql


RUN apt-get update && apt-get install -y wget git zip unzip \
    && pecl install xdebug-2.6.1 \
    && docker-php-ext-enable xdebug

RUN mkdir -p /usr/src/php/ext/uploadprogress; \
    up_url="https://github.com/wodby/pecl-php-uploadprogress/archive/latest.tar.gz"; \
    wget -qO- "${up_url}" | tar xz --strip-components=1 -C /usr/src/php/ext/uploadprogress; \
    docker-php-ext-install uploadprogress;


#RUN apt-get install libwebp-dev libjpeg62-turbo-dev libpng-dev libxpm-dev

RUN apt-get install -y zlib1g-dev libpng-dev \
    && docker-php-ext-install gd \
    && docker-php-ext-install opcache


#RUN docker-php-ext-configure gd --with-gd --with-webp-dir --with-jpeg-dir \
#    --with-png-dir --with-zlib-dir --with-xpm-dir --with-freetype-dir \
#    --enable-gd-native-ttf


ADD ./php.ini /usr/local/etc/php/php.ini

RUN wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer --quiet

WORKDIR /var/www/web
