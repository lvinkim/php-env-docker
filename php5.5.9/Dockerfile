
FROM ubuntu:14.04

# 安装 php5
RUN apt-get update && apt-get install -y \
    php5 \
    php5-cli \
    php5-common \
    php5-dev \
    php5-curl \
    php5-gd \
    php5-json \
    php5-mcrypt \
    php5-xdebug \
    php5-mongo \
    php5-fpm \
    php5-curl \
    php5-redis \
    php-pear \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

# 安装新版 mongodb 扩展
RUN apt-get update && apt-get install -y \
    libpcre3-dev \
  && pecl install mongodb \
  && echo "extension=mongodb.so" >> /etc/php5/mods-available/mongodb.ini \
  && php5enmod mongodb \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

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