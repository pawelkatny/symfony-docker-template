ARG PHP_IMAGE=fpm-alpine
FROM php:${PHP_IMAGE}

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions @composer-2.7.1 apcu amqp bcmath exif gd intl mbstring opcache pcntl pdo pdo_pgsql zip mongodb redis

ARG BUILD_TYPE=prod
ARG PHP_CONFIG_DIR="/usr/local/etc/php/conf.d"
ARG XDEBUG_ON=false
ARG WWW_DATA=""

COPY "./docker/php/config/php.${BUILD_TYPE}.ini" "${PHP_INI_DIR}/php.ini"




RUN if [ "${WWW_DATA}" != "" ]; then					\
    apk add --update --no-cache shadow &&				\
    groupmod --gid ${WWW_DATA#*:} www-data &&				\
    usermod --uid ${WWW_DATA%:*} --gid ${WWW_DATA#*:} www-data &&	\
    apk del shadow;							\
fi

COPY --chown=www-data "." "/var/www/html"

RUN if [ "${XDEBUG_ON}" = "true" ]; then  \
    install-php-extensions xdebug &&	    \
    cp ./docker/php/config/xdebug.ini "${PHP_CONFIG_DIR}/xdebug.ini"; \
fi

RUN rm -rf "/var/www/html/docker"

USER www-data
RUN composer install

ARG USER=root
USER ${USER}
