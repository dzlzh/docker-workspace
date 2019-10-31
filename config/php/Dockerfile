ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine
LABEL maintainer="dzlzh <dzlzh@null.net>"

ARG ALPINE_REPOSITORIES
ARG PHP_REDIS_VERSION

RUN ln -snf /use/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \

    && if [ "${ALPINE_REPOSITORIES}" != "" ]; then \
        sed -i "s/dl-cdn.alpinelinux.org/${ALPINE_REPOSITORIES}/g" /etc/apk/repositories; \
    fi

    && apk add --no-cache autoconf g++ libtool make curl-dev libxml2-dev linux-headers \
    freetype-dev libjpeg-turbo-dev libpng-dev icu-dev bzip2-dev \
    
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \

    && docker-php-ext-install -j$(nproc) pdo_mysql zip pcntl mysqli mbstring exif bcmath \
    opcache sockets pdo_firebird pdo_dblib gd intl bz2 curl \

    && mkdir ridis \
    && wget https://github.com/phpredis/phpredis/archive/${PHP_REDIS_VERSION}.tar.gz \
    && tar -zxf ${PHP_REDIS_VERSION}.tar.gz -C redis \
    && (cd redis && phpize && .configure && make -j$(nproc) && make install) \ 
    && docker-php-ext-enable redis 
    && (cd - && rm -rf redis ${PHP_REDIS_VERSION}.tar.gz)

WORKDIR /var/www/html
