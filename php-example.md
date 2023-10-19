---
layout: default
title: PHP Web Development in Docker
nav_order: 5
---

# PHP Web Development in Docker

PHP is one of the most widely used open source and general purpose server side scripting language to create dynamic websites and applications. It is still commonly used to build many Content Management System (CMS). As such, the PHP community created tremendous support for running PHP web development projects as Docker container. In this example, we will demostrate how you can dockerize your (Laravel Framework based) PHP web development project.  

Create a `docker-compose.yaml` file in the root directory of your Laravel project.  

```conf
services:
    app:
        build: .
        ports:
            - "80:80"
        volumes:
            - ./:/var/www/html
```

Here, we're creating one service named `app`. In this container, we indicate the container's port 80 will be published to the port 80 of our local machine and we will attach the whole Laravel project directory to the container as a volume.

Next, create a `Dockerfile` in the same directory and paste the following content:  

```Dockerfile
FROM php:7.2-apache
WORKDIR /var/www/html
COPY vhost.conf /etc/apache2/sites-available/000-default.conf
RUN apt update && apt install -y \
        nodejs \
        npm \
        libpng-dev \
        zlib1g-dev \
        libxml2-dev \
        libzip-dev \
        libonig-dev \
        zip \
        curl \
        unzip \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-source delete

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN chown -R www-data:www-data /var/www/html && a2enmod rewrite
```

In the `Dockerfile` above, we instruct Docker to retrieve the official PHP 7.2 image with Apache Server. We then set our working directory and install all PHP and project dependencies. Notice there is a `COPY` instruction, which is used to configure the Apache server settings. We will go through the Apache server settings in the next section.  

## Apache Server Virtual Host

Apache service is a popular open-source web server alternative to Nginx. It offers great flexibility and compatibility with PHP. Apache server configuration happens through a modular design where new configuration files can be added and modified as needed. Within this modular design, you can create individual site called a **virtual host**.  

To set up a virutal host for the Laravel project, first create a `vhost.conf` file in the root directory of your project.  

```conf
<VirtualHost *:80>
    DocumentRoot /var/www/html/public

    <Directory "/var/www/html">
        AllowOverride all
        Require all granted
    </Directory>
</VirtualHost>
```