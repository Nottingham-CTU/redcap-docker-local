# Use an official PHP image with Apache as the base image.
FROM php:8.2-apache

# Install system dependencies. We want MySQL CLI so we can communicate with container on socket via Docker from outside.
RUN apt-get update && \
    apt-get install -y git default-mysql-client dos2unix

# Install PHP extensions.  This is key because REDCap uses MySQLi
RUN docker-php-ext-install -j$(nproc) mysqli

# Copy a php.ini
COPY php.ini /usr/local/etc/php

# Set up the entrypoint
COPY ./docker-entrypoint.sh /docker-entrypoint.sh
RUN dos2unix /docker-entrypoint.sh # Required when running on Windows with autocrlf enabled
RUN chmod +x /docker-entrypoint.sh

# Expose port 80 for Apache.
EXPOSE 80

# Start Apache web server.
CMD ["/docker-entrypoint.sh"]