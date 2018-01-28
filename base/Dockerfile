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

RUN apt-key update && apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt-get install -y \
    locate \
    vim \
    git \
    net-tools \
    wget \
    curl \
    apt-transport-https \
    ca-certificates

# Mantain the same user id
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# Phalcon repository
RUN curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash

RUN wget https://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg
RUN apt-get update

# Linux .bashrc
ADD data/.bashrc /root/.bashrc
