FROM php:8.1-cli

WORKDIR /var/www/html

RUN apt-get update -qq && apt-get install -y \
    unzip \
    curl \
    git \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    && docker-php-ext-install pdo_mysql gd mbstring xml

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY . .

RUN composer install --no-dev --optimize-autoloader

RUN npm install

RUN chmod -R 777 storage bootstrap/cache

EXPOSE 8000

CMD  npm run dev -- --host & php artisan serve --host=0.0.0.0 --port=8000  
