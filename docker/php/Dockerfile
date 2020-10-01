FROM wordpress:php7.4-apache

# git
RUN apt-get update && \
    apt-get -y install git

# xdebug
RUN cd /tmp && \
    git clone git://github.com/xdebug/xdebug.git && \
    cd xdebug && \
    git checkout xdebug_2_9 && \
    phpize && \
    ./configure --enable-xdebug && \
    make && \
    make install && \
    rm -rf /tmp/xdebug
RUN docker-php-ext-enable xdebug

# config
COPY docker/php/local.ini /usr/local/etc/php/conf.d/local.ini

# wait for it
COPY docker/bin/wait-for-it.sh /usr/bin/wait-for-it
RUN chmod +x /usr/bin/wait-for-it
CMD wait-for-it db:3306 -t 30 -- apache2-foreground