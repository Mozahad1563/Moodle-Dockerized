# Use PHP 7.4 with Apache
FROM php:7.4-apache

# Install system tools and required PHP extensions
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    libicu-dev \
    mariadb-client \
    && docker-php-ext-install \
    gd \
    mysqli \
    pdo \
    pdo_mysql \
    intl \
    xmlrpc \
    soap \
    mbstring \
    zip \
    opcache

# Enable Apache rewrite module
RUN a2enmod rewrite

# Set working directory
WORKDIR /var/www/html

# Clone Moodle 3.9 from Git
RUN git clone -b MOODLE_39_STABLE git://git.moodle.org/moodle.git

# Create and configure moodledata directory
RUN mkdir -p /var/www/moodledata && \
    chown -R www-data:www-data /var/www/moodledata && \
    chmod -R 775 /var/www/moodledata

# Set file permissions for Moodle directory
RUN chown -R www-data:www-data /var/www/html && \
    chmod -R 755 /var/www/html

# Set PHP configuration directly
RUN echo "opcache.enable=1\n\
opcache.memory_consumption=128\n\
opcache.interned_strings_buffer=8\n\
opcache.max_accelerated_files=10000\n\
opcache.revalidate_freq=1\n\
opcache.validate_timestamps=1" > /usr/local/etc/php/conf.d/opcache-recommended.ini

# Expose Apache port
EXPOSE 80
