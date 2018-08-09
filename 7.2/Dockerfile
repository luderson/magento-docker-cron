FROM php:7.2-cli

# Updating and installing some dependences
# TODO remove suggested packages.
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    libxslt-dev \
    libicu-dev \
    libmemcached-dev \
    zlib1g-dev \
    libmagickwand-dev \
    libmagickcore-dev \
    cron && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install \
    bcmath \
    pdo_mysql \
    xsl \
    intl \
    zip \
    soap \
    gd \
    opcache && \
    apt-get clean -y && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    apt-get purge -y --auto-remove

# Installing pecl PHP modules
RUN pecl install \
    imagick-3.4.3 \
    mcrypt-1.0.1 && \
    docker-php-ext-enable \
    imagick \
    mcrypt

RUN usermod -u 1000 www-data && \
    groupmod -g 1000 www-data && \
    mkdir -p /var/www/ && \
    chown -R www-data:www-data /var/www/ && \
    chmod -R g+w /var/www/

CMD ["cron", "-f"]