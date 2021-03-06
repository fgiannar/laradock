FROM webdevops/apache:ubuntu-16.04

LABEL maintainer="Eric Pfeiffer <computerfr33k@users.noreply.github.com>"

ARG PHP_UPSTREAM_CONTAINER=php-fpm
ARG PHP_UPSTREAM_PORT=9000
ARG PHP_UPSTREAM_TIMEOUT=60
ARG DOCUMENT_ROOT=/var/www/

ENV WEB_PHP_SOCKET=${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}

ENV WEB_DOCUMENT_ROOT=${DOCUMENT_ROOT}

ENV WEB_PHP_TIMEOUT=${PHP_UPSTREAM_TIMEOUT}

EXPOSE 80 443

WORKDIR /var/www/

COPY vhost.conf /etc/apache2/sites-enabled/vhost.conf

RUN mkdir /etc/apache2/ssl 2> /dev/null

RUN openssl genrsa -out "/etc/apache2/ssl/exitbee.key" 2048 \
    && openssl req -new -key "/etc/apache2/ssl/exitbee.key" -out "/etc/apache2/ssl/exitbee.csr" -subj "/CN=wptest.local/O=LGS/C=UK" \
    && openssl x509 -req -days 365 -in "/etc/apache2/ssl/exitbee.csr" -signkey "/etc/apache2/ssl/exitbee.key" -out "/etc/apache2/ssl/exitbee.crt"

RUN service apache2 restart

ENTRYPOINT ["/opt/docker/bin/entrypoint.sh"]

CMD ["supervisord"]
