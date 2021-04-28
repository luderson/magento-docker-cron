FROM php:7.4-cli

# Updating and installing some dependences
# TODO remove suggested packages.
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install --no-install-recommends -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    libxslt-dev \
    libicu-dev \
    libmemcached-dev \
    zlib1g-dev \
    libzip-dev \
    libmagickwand-dev \
    libmagickcore-dev \
    msmtp \
    git \
    nano \
    gnupg \
    cron \
    unzip \
    zip \
    libwebp-dev \
    libcurl4-openssl-dev \
    libonig-dev \
    libsodium-dev && \
    docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp && \
    docker-php-ext-install \
    bcmath \
    # # ctype \
    # curl \
    # # dom \
    gd \
    # # hash \
    # # iconv \
    intl \
    # mbstring \
    # openssl \
    pdo_mysql \
    # simplexml \
    soap \
    xsl \
    zip \
    sockets \
    opcache && \
    # xmlwriter && \
    apt-get clean -y && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    apt-get purge -y --auto-remove
    
# Installing pecl PHP modules
RUN pecl install \
    imagick-3.4.4 \
    libsodium && \
    docker-php-ext-enable \
    imagick

RUN usermod -u 1000 www-data && \
    groupmod -g 1000 www-data && \
    mkdir -p /var/www/ && \
    chown -R www-data:www-data /var/www/ && \
    chmod -R g+w /var/www/

CMD ["cron", "-f"]