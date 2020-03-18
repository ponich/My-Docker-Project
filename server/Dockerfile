FROM ubuntu:latest

# default
ENV TZ=Europe/Kiev
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update
RUN apt-get install -y \
        curl \
        git \
        wget \
        unzip
RUN apt-get autoremove -y

# apache
RUN apt-get install -y apache2
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN a2enmod rewrite

# php
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y php7.4 php7.4-curl php7.4-gd php7.4-json php7.4-mbstring php7.4-mysql php7.4-xml

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD ./src /var/www/
ADD ./services/apache/logs /var/www/logs/
ADD ./services/apache/hosts /etc/apache2/sites-available/


RUN cd /var/www && composer install
RUN chown -R www-data:www-data /var/www
CMD apachectl -D FOREGROUND