FROM php:7.1-fpm

# Install application dependencies
RUN curl --silent --show-error --fail --location \
      --header "Accept: application/tar+gzip, application/x-gzip, application/octet-stream" -o - \
      "https://caddyserver.com/download/linux/amd64?plugins=http.expires,http.realip&license=personal" \
    | tar --no-same-owner -C /usr/bin/ -xz caddy \
    && chmod 0755 /usr/bin/caddy \
    && /usr/bin/caddy -version \
    && docker-php-ext-install mbstring pdo pdo_mysql

COPY ./app /app
COPY docker/Caddyfile /etc/Caddyfile

WORKDIR /app/
RUN chown -R www-data:www-data /app

CMD ["/usr/bin/caddy", "--conf", "/etc/Caddyfile", "--log", "stdout"]

