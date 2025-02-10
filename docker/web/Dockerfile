# Use the official PHP 8.2.14 Apache image as the base
FROM php:8.2.14-apache

# Install Xdebug
RUN pecl install xdebug-3.3.1 && rm -r /tmp/pear/*

# Install required system dependencies
RUN apt-get clean && apt-get update && apt-get install -y \
    libzip-dev \
    zip \
    libicu-dev \
    libxml2-dev \
    libmagickwand-dev \
    --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# Install and enable PHP extensions: Imagick, intl, bcmath, soap, opcache, pdo_mysql, zip, calendar, xdebug
RUN printf "\n" | pecl install imagick && \
    docker-php-ext-install intl bcmath soap opcache pdo_mysql zip calendar && \
    docker-php-ext-enable imagick xdebug

# Copy PHP configuration file
COPY php.ini "$PHP_INI_DIR/php.ini"

# Copy Xdebug configuration file
COPY xdebug.ini "$PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini"

# Enable Apache mod_rewrite module
RUN a2enmod rewrite
