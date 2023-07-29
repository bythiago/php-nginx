FROM php:fpm as builder

ARG USER=dev
ARG UID=1000
ARG NODE_VERSION=16
ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y vim gnupg gosu curl ca-certificates zip unzip git supervisor sqlite3 libcap2-bin libpng-dev \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN groupadd --force -g 1000 www-data

RUN useradd -G www-data,root -u $UID -d /home/$USER $USER
RUN mkdir -p /home/$USER/.composer && \
    mkdir -p /usr/local/lib/node_modules && \
    chown -R $USER:$USER /home/$USER && \
    chown -R $USER:$USER /usr/local/bin /usr/local/lib
    
USER $USER