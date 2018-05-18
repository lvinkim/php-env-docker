
FROM ubuntu:16.04

# 安装 php7.1
RUN apt-get update && apt-get install -y \
    language-pack-en-base \
  && locale-gen en_US.UTF-8 \
  && apt-get install -y \
    software-properties-common \
  && LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php \
  && apt-get update && apt-get install -y \
    php7.1-cli \
    php7.1-fpm \
    php7.1-xml \
    php7.1-mbstring \
    php7.1-curl \
    php7.1-dev \
    php-pear \
    php-xdebug \
    php-mongodb \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

# 安装 composer 相关
RUN apt-get update && apt-get install -y \
    git \
    zip \
    unzip \
    wget \
  && rm -rf /var/lib/apt/lists/* \
  && wget -O /usr/local/bin/composer https://getcomposer.org/download/1.6.2/composer.phar \
  && chmod +x /usr/local/bin/composer

# 安装 librdkafka 以及 php-rdkafka 扩展
RUN apt-get update && apt-get install -y \
    build-essential \
  && cd /opt && git clone https://github.com/edenhill/librdkafka.git \
  && cd /opt/librdkafka \
  && ./configure \
  && make \
  && make install \
  && pecl install rdkafka \
  && echo "extension=rdkafka.so" > /etc/php/7.1/mods-available/rdkafka.ini \
  && phpenmod rdkafka \
  && rm -rf /var/lib/apt/lists/* && apt-get clean \
  && rm -rf /opt/librdkafka

# 安装 swoole
RUN pecl install swoole \
  && echo "extension=swoole.so" > /etc/php/7.1/mods-available/swoole.ini \
  && phpenmod swoole
