FROM nikolaslada/debian-stretch

MAINTAINER Nikolas Lada <nikolas.lada@gmail.com>

ENV PHP_MODS_DIR=/etc/php/7.0/mods-available
ENV PHP_CLI_DIR=/etc/php/7.0/cli/
ENV PHP_CLI_CONF_DIR=${PHP_CLI_DIR}/conf.d

ENV TZ=Europe/Prague

RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        bash-completion \
        wget \
        curl \
        ca-certificates \
        php \
        php-apcu \
        php-bcmath \
        php-bz2 \
        php-cli \
        php-curl \
        php-gd \
        php-geoip \
        php-gettext \
        php-imap \
        php-imagick \
        php-intl \
        php-json \
        php-mbstring \
        php-mcrypt \
        php-mysql \
        php-pgsql \
        php-readline \
        php-redis \
        php-soap \
        php-sqlite3 \
        php-xdebug \
        php-xmlrpc \
        php-zip && \
    apt-get update && \
    cp /etc/skel/.bashrc ~/ && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer global require "hirak/prestissimo:^0.3" && \ 
    apt-get clean -y && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /var/lib/log/* /tmp/* /var/tmp/*

ADD conf.d/devel.ini ${PHP_MODS_DIR}/devel.ini

RUN ln -s ${PHP_MODS_DIR}/devel.ini ${PHP_CLI_CONF_DIR}/100-devel.ini

WORKDIR /srv

CMD ["bash"]
