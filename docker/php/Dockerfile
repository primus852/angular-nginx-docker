FROM php:8.0-fpm

RUN apt-get update --fix-missing
RUN apt-get install -y curl
RUN apt-get install -y build-essential libssl-dev zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev libzip-dev libpq-dev

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
	&& docker-php-ext-install pdo pdo_pgsql pgsql

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install gd

RUN pecl install apcu

RUN docker-php-ext-install zip
RUN docker-php-ext-enable apcu

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Increase Memory Limit
RUN echo 'memory_limit = 2G' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini;

WORKDIR /usr/src/app

COPY --chown=1000:1000 apps/backend /usr/src/app

RUN PATH=$PATH:/usr/src/app/vendor/bin:bin

RUN composer install --no-scripts --prefer-dist \
  && rm -rf "$(composer config cache-dir)" "$(composer config data-dir)"
