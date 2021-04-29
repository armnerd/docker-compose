FROM php:7.4-fpm
WORKDIR "/application"
ENV TIME_ZONE Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone
COPY ./sources.list /etc/apt/sources.list
# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN rm -rf /etc/apt/sources.list.d/* && apt-get update \
    && apt-get install -y --allow-downgrades \
    libzip-dev \
    zlib1g=1:1.2.8.dfsg-5 \
    zlib1g-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo pdo_mysql \
	&& docker-php-ext-install bcmath \
    && apt-get clean \
    && apt-get autoremove --purge -y

# Install Redis extension
RUN curl -L -o /tmp/reids.tar.gz https://codeload.github.com/phpredis/phpredis/tar.gz/5.0.2 \
    && cd /tmp && tar -xzf reids.tar.gz \
    && docker-php-source extract \
    && mv phpredis-5.0.2 /usr/src/php/ext/phpredis \
    && docker-php-ext-install phpredis

