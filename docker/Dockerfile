FROM php:7.1-apache
USER root
WORKDIR /var/www/html
RUN apt-get -y update && apt-get -y upgrade && apt install -y curl zip unzip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
COPY ../happs /var/www/html
COPY .docker/vhost.conf /etc/apache2/sites-available/000-default.conf
RUN composer config --no-plugins allow-plugins.kylekatarnls/update-helper true
RUN composer update
RUN php artisan migrate --seed
