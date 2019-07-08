FROM php:5.6-apache
MAINTAINER Diomedes Pablo <diomedex10@gmail.com>

#instalando buil-essential
RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -yq install \
    build-essential \
    git \
    libpq-dev \
    libssl-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libxml2-dev \
    libcurl4-gnutls-dev \
    mysql-client

#instalando extensiones php
RUN docker-php-ext-install bcmath curl ftp json mbstring mcrypt mysql mysqli pgsql pdo  pdo_mysql pdo_pgsql simplexml calendar\
    soap tokenizer xml zip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

#habilitar configs personalizadas
COPY configs/ /usr/local/etc/php/conf.d/

#copiar vhosts
COPY vhosts/ /etc/apache2/sites-enabled/

#Certificados ssl
ADD ssl/server.crt /etc/apache2/ssl/server.crt
ADD ssl/server.key /etc/apache2/ssl/server.key

#habilitando mod_rewrite
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod headers
RUN a2enmod cache
RUN a2enmod cache_disk
RUN a2enmod expires

#creando directorio para los proyectos
RUN mkdir -p /apps

#RUN service apache2 restart

#volumen y directorio de trabajo
WORKDIR /apps
VOLUME /apps


