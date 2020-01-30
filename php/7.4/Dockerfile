FROM php:7.4-apache

RUN apt-get update && apt-get install -y nano dialog ssl-cert apt-utils mc \
    && a2enmod ssl \
    && a2enmod rewrite

# Install Java & LibreOffice & nano & apt-utils
RUN mkdir -p /usr/share/man/man1 \
    && mkdir -p /var/www/html/public \
    && apt-get update \
    && apt-get install -y --no-install-recommends default-jre libreoffice \
    && apt-get install -y \
        libicu-dev \
        libcurl4-openssl-dev \
        curl \
        git \
        libzip-dev \
        zlib1g-dev \
        libpcre3-dev \
        locales \
        libpng-dev cron \
        unzip \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-configure mysqli --with-mysqli=mysqlnd \
    && docker-php-ext-configure intl
    && docker-php-ext-install pdo_mysql mysqli intl mbstring zip pcntl gd bcmath \
    && locale-gen en_US en_US.UTF-8 sk_SK sk_SK.UTF-8 \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && truncate -s 0 /var/log/*log


RUN dpkg-reconfigure -f noninteractive locales \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && /bin/bash -c 'composer global require phpmd/phpmd phpunit/phpunit' \
    && /bin/bash -c 'curl -L https://cs.symfony.com/download/php-cs-fixer-v2.phar -o /usr/local/bin/php-cs-fixer' \
    && /bin/bash -c 'chmod a+x /usr/local/bin/php-cs-fixer' \
    && touch /var/log/cron.log \
    && chmod 0777 /var/log/cron.log \
    && service apache2 restart

# add composer global libs to PATH
ENV PATH="/root/.composer/vendor/bin:${PATH}"

EXPOSE 443
EXPOSE 80
EXPOSE 9000
