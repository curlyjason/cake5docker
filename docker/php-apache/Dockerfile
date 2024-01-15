FROM php:8.2-apache

COPY . .

EXPOSE 80

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get -y update \
&& apt-get install -y libicu-dev \
    && apt-get install -y libzip-dev

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN docker-php-ext-configure intl

RUN docker-php-ext-install intl

RUN docker-php-ext-install zip

RUN apt install nano

COPY ./docker/php-apache/apache2/sites-enabled/001-site.conf /etc/apache2/sites-available/001-site.conf

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf \
    && a2enmod rewrite \
    && a2dissite 000-default \
    && a2ensite 001-site \
    && service apache2 restart

