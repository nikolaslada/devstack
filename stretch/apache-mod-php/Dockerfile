FROM nikolaslada/debian-stretch

MAINTAINER Nikolas Lada <nikolas.lada@gmail.com>

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data

ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

ENV PHP_MODS_DIR=/etc/php/7.0/mods-available
ENV APACHE_MOD_PHP_DIR=/etc/php/7.0/apache2
ENV APACHE_MOD_PHP_CONF_DIR=${APACHE_MOD_PHP_DIR}/conf.d
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
        apache2 \
        apache2-bin \
        apache2-data \
        apache2-utils \
        php \
        php-apcu \
        php-bcmath \
        php-bz2 \
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
        php-zip \
        libapache2-mod-php && \
    apt-get update && \
    a2enmod include && \
    a2enmod rewrite && \
    a2enmod http2 && \
    a2enmod php7.0 && \
    rm /etc/apache2/sites-enabled/000-default.conf && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer global require "hirak/prestissimo:^0.3" && \ 
    apt-get clean -y && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /var/lib/log/* /tmp/* /var/tmp/*

ADD conf.d/apache2-devel.ini ${PHP_MODS_DIR}/cli-devel.ini
ADD conf.d/cli-devel.ini ${PHP_MODS_DIR}/cli-devel.ini
ADD conf/devel.conf /etc/apache2/conf-enabled/100-devel.conf
ADD sites /etc/apache2/sites-enabled

RUN ln -s ${PHP_MODS_DIR}/apache2-devel.ini ${APACHE_MOD_PHP_CONF_DIR}/100-devel.ini
RUN ln -s ${PHP_MODS_DIR}/cli-devel.ini ${PHP_CLI_CONF_DIR}/100-devel.ini

WORKDIR /srv

EXPOSE 80
EXPOSE 443

CMD ["apache2ctl", "-D FOREGROUND"]
