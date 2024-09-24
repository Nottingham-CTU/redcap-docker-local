# Use an official PHP image with Apache as the base image.
FROM php:8.2-apache

# Install system dependencies. We want MySQL CLI so we can communicate with container on socket via Docker from outside.
RUN apt-get update && \
    apt-get install -y git default-mysql-client

# Install PHP extensions.  This is key because REDCap uses MySQLi
RUN docker-php-ext-install -j$(nproc) mysqli

# Copy a php.ini
COPY php.ini /usr/local/etc/php

# Expose port 80 for Apache.
EXPOSE 80

# Start Apache web server.
CMD ["apache2-foreground"]