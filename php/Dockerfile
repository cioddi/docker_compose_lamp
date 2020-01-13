FROM php:7.2-apache-stretch

COPY php.ini /usr/local/etc/php/
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libgd-dev libmcrypt-dev libzip-dev libxml2-dev libzip4 \
  && docker-php-ext-install pdo_mysql mysqli iconv zip gd 
RUN pear install -a SOAP-0.13.0 \
    && docker-php-ext-install soap;
RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends
RUN apt-get update && apt-get install -y wget curl --no-install-recommends
RUN pecl install imagick && docker-php-ext-enable imagick
RUN pecl install mcrypt-1.0.1 && docker-php-ext-enable mcrypt
#RUN pecl install openssl && docker-php-ext-enable openssl
COPY ./hostconfig.conf  /etc/apache2/sites-available/
COPY ./hosts  /etc/hosts
RUN apt-get update && apt-get install -y ssl-cert imagemagick
RUN apt-get update && apt-get install -y zlib1g-dev libicu-dev g++
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd
#RUN php5enmod imagick 
RUN a2enmod rewrite 
RUN a2enmod headers 
RUN a2enmod ssl

RUN service apache2 restart
RUN a2dissite 000-default.conf 
RUN a2ensite hostconfig.conf 

#WORKDIR /var/www/html
