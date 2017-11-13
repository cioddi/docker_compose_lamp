FROM php:5.6-apache

COPY php.ini /usr/local/etc/php/
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev libmcrypt-dev ssl-cert imagemagick zlib1g-dev libicu-dev g++ \
  && docker-php-ext-install pdo_mysql mysqli iconv zip mcrypt
RUN apt-get install -y libmagickwand-dev --no-install-recommends
RUN pecl install imagick && docker-php-ext-enable imagick
COPY ./hostconfig.conf  /etc/apache2/sites-available/
COPY ./hosts  /etc/hosts

RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd
#RUN php5enmod imagick 
RUN a2enmod rewrite 
RUN a2enmod headers 
RUN a2enmod ssl

RUN service apache2 restart
RUN a2ensite hostconfig.conf 

#WORKDIR /var/www/html
