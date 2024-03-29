FROM php:7.2-fpm-stretch
WORKDIR "/application"
ENV TIME_ZONE Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone
COPY ./sources.list /etc/apt/sources.list
# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN rm -rf /etc/apt/sources.list.d/* && apt-get update && apt-get install -y --no-install-recommends \
        cron \
        procps \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libmemcached-dev \
        graphicsmagick \
        libgraphicsmagick1-dev \
        imagemagick \
        libmagickwand-dev \
        libssh2-1-dev \
        libzip-dev \
        libzookeeper-mt-dev \
        libldap2-dev \
        libssl-dev \
        libmosquitto-dev \
        librabbitmq-dev \
        inotify-tools \
        libevent-dev \
        libhiredis-dev \
        librdkafka-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install -j$(nproc) bcmath gd gettext pdo_mysql mysqli ldap pcntl soap sockets sysvsem xmlrpc \
    && pecl install gmagick-2.0.5RC1 \
    && pecl install imagick-3.4.3 \
    && pecl install memcached-3.0.4 \
    && pecl install redis-4.0.2 \
    && pecl install mcrypt-1.0.1 \
    && pecl install mongodb-1.5.3 \
    && pecl install swoole-4.4.12 \
    && pecl install ssh2-1.1.2 \
    && pecl install yaf-3.0.7 \
    && pecl install yaconf-1.0.7 \
    && pecl install zip-1.15.2 \
    && pecl install zookeeper-0.5.0 \
    && pecl install Mosquitto-0.4.0 \
    && pecl install amqp-1.9.3 \
    && pecl install inotify-2.0.0 \
    && pecl install event-2.3.0 \
    && pecl install xdebug-2.6.0 \
    && pecl install rdkafka-3.0.5 \
    && pecl install grpc-1.19.0 \
    && pecl install protobuf-3.7.1 \
    && pecl install apcu-5.1.17 \
    && docker-php-ext-enable gmagick memcached redis mcrypt mongodb swoole ssh2 yaf yaconf zip zookeeper mosquitto amqp inotify rdkafka grpc protobuf apcu \
    && apt-get clean \
    && apt-get autoremove --purge -y

