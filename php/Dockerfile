FROM php:7.3.33-fpm-alpine3.14

RUN docker-php-ext-install pdo pdo_mysql

#allows super user to user composer in the container
ENV COMPOSER_ALLOW_SUPERUSER=1

# copies composer from composer image to our docker container
COPY --from=composer:2.5.8 /usr/bin/composer /usr/bin/composer

# copies only composer.json and composer.lock before installing composer.
# this will copy from the docker cache and composer installation will only be
# executed if composer.json or composer.loch have changed.

COPY ./app/composer.* ./

# Composer Installation
RUN composer install --prefer-dist --no-dev --no-scripts --no-progress --no-interaction

# Copy application files to working directory
COPY ./app .

RUN composer dump-autoload --optimize