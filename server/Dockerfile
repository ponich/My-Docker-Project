FROM ubuntu:latest
# default
RUN apt update && apt upgrade
RUN apt-get update && apt-get install -y \
        curl \
        git \
        wget \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libc-client-dev \
        libkrb5-dev \
        libpng-dev \
        zlib1g-dev \
        libicu-dev \
        unzip \
        gnupg \
        g++
RUN apt-get autoremove -y

# apache
RUN apt-get install apache2

# php
RUN apt-get install software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install php7.4 php7.4-curl php7.4-gd php7.4-json php7.4-mbstring php7.4-mysql php7.4-xml

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

ADD ./src /var/www

WORKDIR /var/www/
