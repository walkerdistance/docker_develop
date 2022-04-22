FROM php:7.2-fpm

RUN apt-get update -yqq && \
    pecl channel-update pecl.php.net && \
    apt-get install -y apt-utils openssl libssl-dev && \
    apt-get install libzip-dev zlib1g-dev zip unzip -y && \
    docker-php-ext-configure zip --with-libzip && \
    apt-get install -y libmagickwand-dev imagemagick && pecl install imagick && docker-php-ext-enable imagick && \
    apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev && \
    docker-php-ext-install -j$(nproc) iconv && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd && \
    docker-php-ext-install pdo && rm -rf /temp/pear && docker-php-ext-enable pdo && \
    docker-php-ext-install mysqli && rm -rf /temp/pear && docker-php-ext-enable mysqli && \
    docker-php-ext-install pdo_mysql && rm -rf /temp/pear && docker-php-ext-enable pdo_mysql && \
    docker-php-ext-install zip && rm -rf /temp/pear && docker-php-ext-enable zip && \
    docker-php-ext-install pcntl && rm -rf /temp/pear && docker-php-ext-enable pcntl && \
    pecl install redis &&  rm -rf /tmp/pear &&  docker-php-ext-enable redis && \
    pecl install swoole &&  rm -rf /tmp/pear && docker-php-ext-enable swoole && \
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/bin/composer && \
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
