FROM lorisleiva/laravel-docker:8.1

WORKDIR /app
COPY composer.* package.json ./
RUN composer install --prefer-dist --no-ansi --no-interaction --no-progress --no-scripts
COPY . .
RUN php artisan key:generate
RUN php artisan jwt:secret

RUN rm -rf .env
CMD [ "php", "artisan", "serve", "--host=0.0.0.0" ]
