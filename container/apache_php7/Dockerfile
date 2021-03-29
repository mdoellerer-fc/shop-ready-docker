FROM php:7.3-apache

MAINTAINER module@proudcommerce.com

# timezone / date   
RUN echo "Europe/Berlin" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata

# install packages
RUN apt-get update -y && \
  apt-get install -y --no-install-recommends \
  less vim wget unzip rsync git default-mysql-client libzip-dev ssl-cert \
  libcurl4-openssl-dev libfreetype6 libjpeg62-turbo libpng-dev libjpeg-dev libxml2-dev libxpm4 && \
  apt-get clean && \
  apt-get autoremove -y && \
  rm -rf /var/lib/apt/lists/* && \
  echo "export TERM=xterm" >> /root/.bashrc

# install php extensions
RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/local/ && \
  docker-php-ext-install -j$(nproc) zip bcmath soap pdo_mysql gd

# xdebug
RUN yes | pecl install xdebug \
  && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
  && echo "[XDebug]" >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo "xdebug.client_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo "xdebug.remote_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
  && echo "xdebug.discover_client_host=127.0.0.1" >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo "xdebug.idekey=xdebug" >> /usr/local/etc/php/conf.d/xdebug.ini

# composer stuff
RUN php -r 'readfile("https://getcomposer.org/installer");' > composer-setup.php \
  && php composer-setup.php --1 --install-dir=/usr/local/bin --filename=composer \
  && rm -f composer-setup.php \
  && chown www-data:www-data /var/www


# apache stuff
RUN /usr/sbin/a2enmod rewrite && /usr/sbin/a2enmod headers && /usr/sbin/a2enmod expires && /usr/sbin/a2enmod ssl
COPY ./files/000-default.conf /etc/apache2/sites-available/000-default.conf

CMD ["apache2-foreground"]
