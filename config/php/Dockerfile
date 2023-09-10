FROM php:7.4-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
        sudo \
        curl \
        wget \
        git \
        unzip \
        zip \
        mc \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
		libzip-dev \
#        openssh-client \
    && docker-php-ext-install -j$(nproc) iconv mysqli pdo_mysql zip \
    && docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-freetype=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

#CMD ssh-keygen -q -t rsa -N '' -f /keys/id_rsa
    
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
RUN apt-get install symfony-cli

RUN adduser --disabled-password --gecos '' alexander \
    && adduser alexander sudo \
    && echo '%sudo ALL=(ALL:ALL) ALL' >> /etc/sudoers

USER alexander

WORKDIR /var/www/project

CMD ["php-fpm"]
