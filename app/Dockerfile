FROM ubuntu:xenial
MAINTAINER santteegt

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
        && apt-get install -q -y net-tools curl git apache2 php mysql-server \
        && service apache2 start \
        && apt-get install -y php-bcmath php-bz2 php-intl php-gd php-mbstring php-mcrypt php-zip php-curl php-mysql php-cgi \
        php-cli php-common php-dev php-gd \
        && apt-get install -y libapache2-mod-php \
        && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY ./runapache.sh /root/runapache.sh

RUN chmod +x /root/runapache.sh

RUN a2enmod rewrite
RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

EXPOSE 80

ENTRYPOINT ["/root/runapache.sh"]