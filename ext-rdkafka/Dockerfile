
FROM lvinkim/php-env-docker:latest

# 安装 librdkafka 以及 php-rdkafka 扩展
RUN apt-get update && apt-get install -y \
    build-essential \
  && cd /opt && git clone https://github.com/edenhill/librdkafka.git \
  && cd /opt/librdkafka \
  && ./configure \
  && make \
  && make install \
  && pecl install rdkafka \
  && echo "extension=rdkafka.so" > /etc/php/7.2/mods-available/rdkafka.ini \
  && phpenmod rdkafka \
  && rm -rf /var/lib/apt/lists/* && apt-get clean \
  && rm -rf /opt/librdkafka