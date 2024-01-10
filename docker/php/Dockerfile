FROM php:8.2-fpm

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get -y update \
&& apt-get install -y libicu-dev \
    && apt-get install -y libzip-dev

RUN docker-php-ext-configure intl

RUN docker-php-ext-install intl

RUN docker-php-ext-install zip

# allow super user - set this if you use Composer as a
# super user at all times like in docker containers
ENV COMPOSER_ALLOW_SUPERUSER=1

# obtain composer using multi-stage build
# https://docs.docker.com/build/building/multi-stage/
COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

#Here, we are copying only composer.json and composer.lock (instead of copying the entire source)
# right before doing composer install.
# This is enough to take advantage of docker cache and composer install will
# be executed only when composer.json or composer.lock have indeed changed!-
# https://medium.com/@softius/faster-docker-builds-with-composer-install-b4d2b15d0fff
COPY ./composer.* ./

# install
RUN composer install --prefer-dist --no-dev --no-scripts --no-progress --no-interaction

# copy application files to the working directory
COPY ./ .

# run composer dump-autoload --optimize
RUN composer dump-autoload --optimize
