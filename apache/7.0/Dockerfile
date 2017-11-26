FROM debian:jessie
MAINTAINER Mateus Schmitz <matteuschmitz@gmail.com>

RUN echo "deb http://debian.pop-sc.rnp.br/debian/ jessie main contrib non-free" > /etc/apt/sources.list
RUN echo "deb-src http://debian.pop-sc.rnp.br/debian/ jessie main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://security.debian.org jessie/updates main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://security.debian.org jessie/updates main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list
RUN echo "deb-src http://packages.dotdeb.org jessie all"  >> /etc/apt/sources.list

RUN gpg --keyserver keys.gnupg.net --recv-key 89DF5277
RUN gpg -a --export 89DF5277 | apt-key add -

RUN apt-key update
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get dist-upgrade -y
RUN apt-get install -y \
    locate \
    apache2 \
    vim \
    git \
    net-tools \
    wget \
    curl \
    php7.0 \
    php7.0-mysql \
    php7.0-mcrypt \
    php7.0-curl \
    php7.0-dom

RUN wget https://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg
RUN apt-get update

RUN service apache2 stop
RUN a2enmod rewrite
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# instala o Phalcon
RUN curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash
RUN apt-get install php7.0-phalcon -y

# PHP ini
ADD data/php/php.ini /etc/php/7.0/apache2/php.ini
ADD data/php/php.ini /etc/php/7.0/cli/php.ini

# PHPINFO
ADD data/php/index.php /var/www/html/index.php

# Logs
RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stderr /var/log/apache2/error.log

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
