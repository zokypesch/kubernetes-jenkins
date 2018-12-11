# docker build . -t my-php-app:1.0.0

FROM php:7.0-fpm

# Install modules
RUN buildDeps="libpq-dev libzip-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libgmp-dev git openssh-client vim " \
    && apt-get update && apt-get install -y $buildDeps --no-install-recommends \
    && pecl install -o -f redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install gmp \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install pdo_pgsql pgsql gd \
    && docker-php-ext-install pdo pdo_mysql gd \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN curl -sSL https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && apt-get install -y zlib1g-dev git wget \
    && docker-php-ext-install zip \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /app
COPY hello.php /app