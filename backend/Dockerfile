FROM php:7-apache

ARG DIRECTUS_VERSION

RUN apt-get update && apt-get install -y \
  libjpeg-dev \
  libpng-dev

# Configure Apache
COPY apache/virtualhost.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite

# Configure PHP
COPY php/uploads.ini /usr/local/etc/php/conf.d/uploads.ini

# Configure PHP extensions
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr

# Install PHP extensions
RUN docker-php-ext-install gd mbstring pdo_mysql

# Download and extract Directus
RUN curl -SL https://github.com/directus/directus/archive/${DIRECTUS_VERSION}.tar.gz | tar -xz --strip-components=1
RUN chown -R www-data:www-data /var/www/html

CMD ["apache2-foreground"]
