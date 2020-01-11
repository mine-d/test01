FROM php:7.1-apache

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
        # for gd
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libwebp-dev \
        libxpm-dev \
        # from zip
        zlib1g-dev iputils-ping net-tools zip unzip git && \
    docker-php-ext-install exif mbstring mysqli pdo pdo_mysql zip && \
    docker-php-ext-install -j$(nproc) iconv && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    # enable mod_rewrite
    a2enmod rewrite

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN mkdir /mine /mine_data
