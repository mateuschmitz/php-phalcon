FROM mateuschmitz/php-phalcon:base
MAINTAINER Mateus Schmitz <matteuschmitz@gmail.com>

# PHP Repository
RUN echo "deb https://packages.sury.org/php/ jessie main" > /etc/apt/sources.list.d/php.list
RUN apt-get update

# install Apache, PHP e Phalcon 
RUN apt-get install -y --force-yes \
    locate \
    apache2 \
    php7.2 \
    php7.2-mysql \
    php7.2-curl \
    php7.2-dom \
    php7.2-phalcon


RUN service apache2 stop
RUN a2enmod rewrite
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# PHP ini
ADD data/php.ini /etc/php/7.0/apache2/php.ini
ADD data/php.ini /etc/php/7.0/cli/php.ini

# PHPINFO
ADD data/index.php /var/www/html/index.php
RUN rm /var/www/html/index.html

# Logs
RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stderr /var/log/apache2/error.log

WORKDIR '/var/www/html'
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
