# This dockerfile uses the php image
# Yii2 Test - 7.0
# Author: Larry Li

FROM php:7.0.7
MAINTAINER Larry Li larryli@qq.com

RUN echo 'expose_php=off' >> /usr/local/etc/php/conf.d/off-expose.ini
RUN set -xe \
	&& buildDeps=" \
        libicu-dev \
        libpq-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmagickwand-dev \
        libmemcached-dev \
	" \
    && apt-get update && apt-get install -y \
		git \
        unzip \
        libicu52 \
        libpq5 \
        libfreetype6 \
        libjpeg62-turbo \
        libmagickwand-6.q16-2 \
        libmemcachedutil2 \
        $buildDeps \
	--no-install-recommends && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-install intl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr/include/freetype2 \
    --with-png-dir=/usr/include \
    --with-jpeg-dir=/usr/include \
    && docker-php-ext-install gd \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && cd /tmp \
    && echo "Download php7 memcached from GitHub" \
    && curl -sO https://codeload.github.com/php-memcached-dev/php-memcached/zip/php7 \
    && unzip php7 \
    && cd php-memcached-php7 \
    && phpize \
    && ./configure \
    && make install \
    && cd / && rm -rf /tmp/php-memcached-php7 \
    && docker-php-ext-enable memcached \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false \
        $buildDeps \
    && rm -rf /tmp/pear
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '070854512ef404f16bac87071a6db9fd9721da1684cd4589b1196c3faf71b9a2682e2311b36a5079825e155ac7ce150d') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/local/bin \
    && php -r "unlink('composer-setup.php');" \
    && mkdir /usr/local/etc/php/conf.dis \
    && echo '#!/bin/bash' > /usr/local/bin/composer \
    && echo 'function composer() { COMPOSER="$(which composer.phar)" || { echo "Could not find composer in path" >&2 ; return 1 ; } && mv /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.dis ; $COMPOSER "$@" ; STATUS=$? ; mv /usr/local/etc/php/conf.dis/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d ; return $STATUS ; }' >> /usr/local/bin/composer \
    && echo 'composer $@' >> /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
    && composer global require --prefer-dist --no-progress "fxp/composer-asset-plugin:~1.1.1" \
    && composer global require --prefer-dist --no-progress  "codeception/codeception=2.0.*" "codeception/specify=*" "codeception/verify=*" \
    && ln -s -f /root/.composer/vendor/bin/* /usr/local/bin/ \
    && rm -rf /root/.composer/cache

CMD ["php", "-a"]
