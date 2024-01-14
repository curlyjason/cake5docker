FROM php:8.2-apache
#WORKDIR /var/www/html

COPY . .
#COPY ./src/ src
EXPOSE 80

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get -y update \
&& apt-get install -y libicu-dev \
    && apt-get install -y libzip-dev

RUN docker-php-ext-configure intl

RUN docker-php-ext-install intl

RUN docker-php-ext-install zip

