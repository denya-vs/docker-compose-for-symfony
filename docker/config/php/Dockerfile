FROM php:7-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        git \
    && docker-php-ext-install -j$(nproc) iconv pdo_mysql opcache\
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install xdebug-2.5.0 \
    && docker-php-ext-enable xdebug

# Install Composer and make it available in the PATH
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

RUN usermod -u 1000 www-data

##Enable remote SSH connetction
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:root2' > /root/passwdfile
RUN cat /root/passwdfile | chpasswd
RUN sed -i 's/^#*\(PermitRootLogin\) .*/\1 yes/' /etc/ssh/sshd_config


EXPOSE 22
CMD /usr/sbin/sshd -D & /usr/local/sbin/php-fpm --nodaemonize

WORKDIR /var/www/web