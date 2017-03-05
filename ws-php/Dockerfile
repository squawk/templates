FROM cloud9/workspace
MAINTAINER Cloud9 IDE, inc. <info@c9.io>

ADD ./files/home /home/ubuntu

RUN bash -c 'chmod -R g+w /home/ubuntu/{workspace,sessions} && \
    chown -R ubuntu:ubuntu /home/ubuntu/{workspace,sessions}'

# PHP based on defaults from
#   http://docs.travis-ci.com/user/ci-environment/#Extensions
#   https://devcenter.heroku.com/articles/php-support
# Xdebug, most recent PECL version
ADD ./files/etc/php7.1 /etc/php7.1
RUN apt-get update || apt-get update
RUN apt-get install -y php7.1 php7.1-cli php7.1-fpm \
        php7.1-curl php7.1-gd php7.1-json php7.1-pgsql php7.1-readline php7.1-sqlite \
        php7.1-tidy php7.1-xmlrpc php7.1-xsl php7.1-intl php7.1-mcrypt php7.1-mysqlnd \
        php-pear \
    && apt-get install -y php7.1-dev \
        && pecl install xdebug \
        && php7enmod xdebug \
    && cd /etc/php7.1/mods-available && ls *.ini | sed 's/\.ini$//' | xargs php7enmod
RUN chown -R ubuntu: /home/ubuntu/lib

ADD ./files/check-environment /.check-environment/php
