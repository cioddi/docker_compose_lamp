FROM php:5.6-apache

COPY php.ini /usr/local/etc/php/
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev libmcrypt-dev \
  && docker-php-ext-install pdo_mysql mysqli gd iconv 
COPY ./hostconfig.conf  /etc/apache2/sites-available/
COPY ./hosts  /etc/hosts
RUN a2enmod rewrite 

RUN service apache2 restart
RUN a2ensite hostconfig.conf 

#WORKDIR /var/www/html

