FROM mateuschmitz/php-phalcon:base
MAINTAINER Mateus Schmitz <matteuschmitz@gmail.com>

# install Apache, PHP e Phalcon 
RUN apt-get install -y \
    locate \
    apache2 \
    php7.0 \
    php7.0-mysql \
    php7.0-mcrypt \
    php7.0-curl \
    php7.0-dom \
    php7.0-phalcon

RUN service apache2 stop
RUN a2enmod rewrite

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
