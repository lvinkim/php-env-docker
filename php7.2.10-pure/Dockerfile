
FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

## 设置时区
RUN echo "tzdata tzdata/Areas select Asia" > /tmp/preseed.txt \
  && echo "tzdata tzdata/Zones/Asia select Shanghai" >> /tmp/preseed.txt \
  && debconf-set-selections /tmp/preseed.txt  \
  && apt-get update && apt-get install -y \
    tzdata \
  && rm -rf /var/lib/apt/lists/* && apt-get clean

## 安装 php
RUN apt-get update && apt-get install -y \
    php \
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

