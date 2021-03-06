
FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

## preesed tzdata, update package index, upgrade packages and install needed software
RUN echo "tzdata tzdata/Areas select Asia" > /tmp/preseed.txt \
  && echo "tzdata tzdata/Zones/Asia select Shanghai" >> /tmp/preseed.txt \
  && debconf-set-selections /tmp/preseed.txt  \
  && apt-get update && apt-get install -y \
    tzdata \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

# 安装 php7.2
RUN apt-get update && apt-get install -y \
    php \
    php-cli \
    php-fpm \
    php-xml \
    php-mbstring \
    php-curl \
    php-dev \
    php-pear \
    php-xdebug \
    php-redis \
    php-zip \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

# 安装新版 mongodb 扩展
RUN pecl install mongodb \
  && echo "extension=mongodb.so" >> /etc/php/7.2/mods-available/mongodb.ini \
  && phpenmod mongodb

# 安装 composer 相关
RUN apt-get update && apt-get install -y \
    git \
    zip \
    unzip \
    wget \
  && rm -rf /var/lib/apt/lists/* && apt-get clean \
  && wget -O /usr/local/bin/composer https://getcomposer.org/download/1.6.2/composer.phar \
  && chmod +x /usr/local/bin/composer

# 安装 nginx
RUN apt-get update && apt-get install -y \
    nginx \
    net-tools \
    telnet \
    curl \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

# 补充 mysql 扩展
RUN apt-get update && apt-get install -y \
    php-mysql \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

# 安装 swoole 扩展
RUN pecl install swoole \
  && echo "extension=swoole.so" > /etc/php/7.2/mods-available/swoole.ini \
  && phpenmod swoole

# 安装 gd 扩展
RUN apt-get update && apt-get install -y \
    php-gd \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

# 安装 rdkafka 扩展
RUN apt-get update && apt-get install -y \
    librdkafka-dev \
  && pecl install rdkafka \
  && echo "extension=rdkafka.so" > /etc/php/7.2/mods-available/rdkafka.ini \
  && phpenmod rdkafka \
  && rm -rf /var/lib/apt/lists/* && apt-get clean
