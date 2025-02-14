FROM php:8.1-cli

# Set working directory
WORKDIR /var/www/html

# Install system dependencies
RUN apt-get update -qq && apt-get install -y \
    unzip \
    curl \
    git \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    && docker-php-ext-install pdo_mysql gd mbstring xml

# Install Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy application files
COPY . .

# Install PHP dependencies
RUN composer install --no-dev --optimize-autoloader

# Install JavaScript dependencies
RUN npm install

# Ensure cache directories are writable
RUN chmod -R 777 storage bootstrap/cache

# Expose application port 
EXPOSE 8000

# Command to run Laravel's built-in server
#CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
CMD php artisan serve --host=0.0.0.0 --port=8000 & npm run dev -- --host
