FROM php:8.1-apache
COPY ./ /var/www
WORKDIR /var/www
RUN apt-get update && apt-get install -y \
        libfreetype6-dev libjpeg62-turbo-dev libpng-dev libicu-dev libmemcached-dev libbz2-dev \
        libssl-dev librabbitmq-dev libxml2-dev libxslt1.1 libxslt1-dev libzip-dev libpq-dev \
        libssh2-1-dev unzip libc-client-dev libkrb5-dev libtidy-dev git subversion mc iputils-ping \
    && a2enmod rewrite \
    && docker-php-ext-configure zip \
    && docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && printf "\n" | pecl install -o -f redis \
    printf "\n" | curl 'http://pecl.php.net/get/redis-5.3.7.tgz' -o redis-5.3.7.tgz \
    && pecl install redis-5.3.7.tgz \
    &&  rm -rf redis-5.3.7.tgz \
    &&  rm -rf /tmp/pear \
    && printf "\n" | pecl install -o -f memcached \
    printf "\n" | curl 'http://pecl.php.net/get/memcached-3.2.0.tgz' -o memcached-3.2.0.tgz \
    && pecl install memcached-3.2.0.tgz \
    &&  rm -rf memcached-3.2.0.tgz \
    &&  rm -rf /tmp/pear \
    && printf "\n" | pecl install -o -f memcache \
    printf "\n" | curl 'http://pecl.php.net/get/memcache-8.0.tgz' -o memcache-8.0.tgz \
    && pecl install memcache-8.0.tgz \
    &&  rm -rf memcache-8.0.tgz \
    &&  rm -rf /tmp/pear \
    && printf "\n" | pecl install -o -f mongodb \
    printf "\n" | curl 'http://pecl.php.net/get/mongodb-1.13.0.tgz' -o mongodb-1.13.0.tgz \
    && pecl install mongodb-1.13.0.tgz \
    &&  rm -rf mongodb-1.13.0.tgz \
    &&  rm -rf /tmp/pear \
    && printf "\n" | pecl install -o -f amqp \
    printf "\n" | curl 'http://pecl.php.net/get/amqp-1.11.0.tgz' -o amqp-1.11.0.tgz \
    && pecl install amqp-1.11.0.tgz \
    &&  rm -rf amqp-1.11.0.tgz \
    &&  rm -rf /tmp/pear \
    && printf "\n" | pecl install xdebug-3.1.4 \
    && printf "\n" | pecl install dbase \
    && printf "\n" | pecl install swoole \
    && printf "\n" | pecl install ssh2-1.3.1 \
    && docker-php-ext-enable redis memcached memcache mongodb amqp xdebug dbase swoole \
    && docker-php-ext-install bcmath bz2 calendar exif opcache mysqli pdo_mysql pgsql pdo_pgsql intl zip soap gd xsl pcntl sockets imap tidy \
    && a2enmod ssl \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && chmod 777 /var/log