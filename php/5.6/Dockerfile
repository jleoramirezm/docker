FROM php:alpine AS cacert

FROM php:5.6-apache

COPY --from=cacert /etc/ssl /root/ssl
RUN mv /etc/ssl/openssl.cnf* /root/ssl && rm -rf /etc/ssl && mv /root/ssl /etc/ssl \
  && pear update-channels \
  && pear upgrade

#Update stretch repositories
RUN sed -i s/deb.debian.org/archive.debian.org/g /etc/apt/sources.list
RUN sed -i 's|security.debian.org|archive.debian.org/|g' /etc/apt/sources.list
RUN sed -i '/stretch-updates/d' /etc/apt/sources.list

#install essentials
RUN apt-get update; \
  apt-get install -y wget; \
  apt-get install -y libcurl3-dev; \
  apt-get install -y libssl-dev; \
  apt-get install -y sudo; \
  apt-get install -y git; \
  apt-get install -y systemd; \
  apt-get install -y unzip; \
  apt-get install -y nano; \
  apt-get install -y zip unzip libzip-dev zlib1g-dev libpng-dev libxml2-dev; \
  docker-php-ext-install gd zip pdo pdo_mysql soap xml mysql mysqli

RUN pear install -f PEAR-1.9.5 \
  && pear install MDB2 \
  && pear install MDB2_Driver_mysqli 