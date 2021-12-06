FROM php:7.3-fpm-alpine

EXPOSE 8080 9000

RUN apk add --no-cache --update --virtual .build-deps $PHPIZE_DEPS libzip-dev
RUN docker-php-ext-install pdo_mysql zip
RUN pecl install redis
RUN docker-php-ext-enable redis
RUN apk del .build-deps
RUN apk add php-zip

WORKDIR /var/www/app
COPY . /var/www/app
RUN chmod -R 777 /var/www/app

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer  --version=2.1.14

RUN composer install --no-plugins --no-scripts

CMD ["php-fpm"]