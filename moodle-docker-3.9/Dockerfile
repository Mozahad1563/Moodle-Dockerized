FROM php:7.4-apache

# Install system dependencies and PHP extensions
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
    default-mysql-client \
    && docker-php-ext-install \
    gd \
    mysqli \
    pdo \
    pdo_mysql \
    intl \
    soap \
    mbstring \
    zip \
    opcache \
    && apt-get clean
# Enable Apache rewrite module
RUN a2enmod rewrite

# Increase PHP limits
RUN echo "upload_max_filesize=128M\n\
post_max_size=128M\n\
memory_limit=256M" > /usr/local/etc/php/conf.d/uploads.ini

# Set timezone
RUN echo "date.timezone=Asia/Dhaka" > /usr/local/etc/php/conf.d/timezone.ini

# Recommended OPcache settings
RUN echo "opcache.enable=1\n\
opcache.memory_consumption=128\n\
opcache.interned_strings_buffer=8\n\
opcache.max_accelerated_files=10000\n\
opcache.revalidate_freq=1\n\
opcache.validate_timestamps=1" > /usr/local/etc/php/conf.d/opcache-recommended.ini

# Set working directory
WORKDIR /var/www/html

# Clone Moodle (optional: you can use COPY if you already have the source)
RUN git clone -b MOODLE_39_STABLE --depth 1 git://git.moodle.org/moodle.git .

# Create Moodle data directory
RUN mkdir -p /var/www/moodledata && \
    chown -R www-data:www-data /var/www/moodledata /var/www/html && \
    chmod -R 755 /var/www/html

# Expose web port
EXPOSE 80
