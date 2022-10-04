FROM php:8.1-apache

RUN apt-get update -y

ARG APACHE_INTERNAL_PORT
ARG MYSQL_DEFAULT_USER
ARG MYSQL_ROOT_PASSWORD
ARG MYSQL_DATABASE

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

WORKDIR /var/www/html
COPY . .

RUN sed -i -e "s/Listen 80/Listen 8008/g" /etc/apache2/ports.conf
RUN cat /etc/apache2/ports.conf
RUN sed -i -e 's/localhost/db/g' /var/www/html/db.php
RUN sed -i -e 's/root/${MYSQL_DEFAULT_USER}/g' /var/www/html/db.php
RUN sed -i -e 's/password123/${MYSQL_ROOT_PASSWORD}/g' /var/www/html/db.php
RUN cat /var/www/html/db.php
CMD ["apachectl", "-D", "FOREGROUND"]
