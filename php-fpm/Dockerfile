FROM php:7.3-fpm

ARG USER_ID=1000
ARG GROUP_ID=1000



ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="10000" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="192" \
    PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

RUN apt-get update

RUN apt-get install -y build-essential make libssl-dev libzip-dev zlib1g-dev libpq-dev libpng-dev git libicu-dev libxml2-dev libjpeg-dev libfreetype6-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install zip xml \
    && pecl install redis-5.1.1 \
    && pecl install xdebug-2.8.1 \
    && docker-php-ext-enable redis xdebug

RUN curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer

RUN docker-php-ext-install opcache
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

ADD conf/opcache.ini "$PHP_INI_DIR/conf.d/opcache.ini"
# Set timezone
#RUN rm /etc/localtime
#RUN ln -s /usr/share/zoneinfo/Europe/Berlin /etc/localtime
#RUN "date"


# node
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
      && apt-get install -y nodejs

# update npm to last version
RUN npm i -g npm

# yarn
RUN curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
     && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
     && apt-get update && apt-get install yarn

RUN npm install --global gulp

RUN /usr/bin/composer self-update

#RUN userdel -f www-data &&\
#    if getent group www-data ; then groupdel www-data; fi &&\
#    groupadd -g ${GROUP_ID} www-data &&\
#    useradd -l -u ${USER_ID} -g www-data www-data &&\
#    install -d -m 0755 -o www-data -g www-data /home/www-data &&\
#    chown --changes --silent --no-dereference --recursive \
#          --from=33:33 ${USER_ID}:${GROUP_ID} \
#        /home/www-data \
#        /.composer \
#        /var/run/php-fpm \
#        /var/lib/php/sessions
#
#USER www-data

RUN addgroup --gid 1000 user
RUN adduser --disabled-password --gecos '' --uid 1000 --gid 1000 user
USER user

WORKDIR /var/www/symfony
