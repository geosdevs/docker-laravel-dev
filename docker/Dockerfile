FROM php:7.4.10-apache

RUN apt-get update && apt-get install -y libicu-dev
RUN docker-php-ext-install intl

RUN apt-get install -y libzip-dev unzip
RUN docker-php-ext-install zip

RUN pecl install xdebug-2.9.6 && docker-php-ext-enable xdebug

RUN docker-php-ext-install pdo_mysql && docker-php-ext-enable pdo_mysql

RUN a2enmod rewrite

RUN apt-get install -y git

WORKDIR /opt

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && ln -s /opt/composer.phar /usr/bin/composer

WORKDIR /var/www/html
RUN mkdir -m775 /var/www/html/storage/ && chown -R www-data:www-data /var/www/html/storage/
VOLUME /var/www/html/

COPY php.ini /usr/local/etc/php/conf.d/docker-laravel-dev.ini
COPY vhost.conf /etc/apache2/sites-enabled/010-laravel.conf
