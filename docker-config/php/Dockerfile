ARG PHP_IMAGE

FROM $PHP_IMAGE

RUN apt-get update \
    && \
    # apt Debian packages
    apt-get install -y \
        apt-utils \
        autoconf \
        ca-certificates \
        curl \
        g++ \
        libbz2-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libonig-dev \
        libpng-dev \
        libpq-dev \
        libssl-dev \
        libicu-dev \
        libmagickwand-dev \
        libzip-dev \
        python-pip \
        python-setuptools \
        unzip \
        wget \
        vim \
        zip \
    && \
    # pecl PHP extensions
    pecl install \
        imagick-3.4.4 \
        redis \
        xdebug-2.8.1 \
    && \
    # Configure PHP extensions
    docker-php-ext-configure \
        gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && \
    # Install PHP extensions
    docker-php-ext-install \
        bcmath \
        bz2 \
        exif \
        ftp \
        gettext \
        gd \
        iconv \
        intl \
        mbstring \
        opcache \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        shmop \
        sockets \
        sysvmsg \
        sysvsem \
        sysvshm \
        zip \
    && \
    # Enable PHP extensions
    docker-php-ext-enable \
        imagick \
        redis \
        xdebug \
    && \
    # Install Composer
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && \
    # Install AWS CLI
    pip install awscli

# Append our php.ini overrides to the end of the file
RUN echo "upload_max_filesize = 10M" > /usr/local/etc/php/php.ini && \
    echo "post_max_size = 10M" >> /usr/local/etc/php/php.ini && \
    echo "max_execution_time = 300" >> /usr/local/etc/php/php.ini && \
    echo "memory_limit = 256M" >> /usr/local/etc/php/php.ini && \
    echo "opcache.revalidate_freq = 0" >> /usr/local/etc/php/php.ini && \
    echo "opcache.validate_timestamps = 1" >> /usr/local/etc/php/php.ini && \
    echo "xdebug.remote_enable = 1" >> /usr/local/etc/php/php.ini

# Copy the `zzz-docker.conf` file into place for php-fpm
COPY ./docker-config/php/zzz-docker.conf /usr/local/etc/php-fpm.d/zzz-docker.conf

WORKDIR /var/www

# Copy over the directories/files php needs access to
COPY --chown=www-data:www-data ./src/composer.* /var/www/src/

WORKDIR /var/www/src

# Do a `composer install` without running any Composer scripts
# - If `composer.lock` is present, it will install what is in the lock file
# - If `composer.lock` is missing, it will update to the latest dependencies
#   and create the `composer.lock` file
# Force permissions, update Craft, and start php-fpm
CMD if [ ! -f "./composer.lock" ]; then \
        composer install --no-scripts --optimize-autoloader --no-interaction; \
    fi \
    && \
    if [ ! -d ./vendor -o ! "$(ls -A ./vendor)" ]; then \
        composer install --no-scripts --optimize-autoloader --no-interaction; \
    fi \
    && \
    chown -R www-data:www-data /var/www/src/vendor \
    && \
    php-fpm
