FROM php:8.1-cli

# Set working directory
WORKDIR /var/www/html

# Install system dependencies (without npm)
RUN apt-get update -qq && apt-get install -y \
    unzip \
    curl \
    git \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    && docker-php-ext-install pdo_mysql gd mbstring xml

# Install Node.js (which includes npm)
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs

# Install Composer globally
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy application files
COPY . .

# Install PHP dependencies
RUN composer install --no-dev --optimize-autoloader

# Install JavaScript dependencies
RUN npm install

# Ensure storage and cache directories are writable
RUN chmod -R 777 storage bootstrap/cache

# Expose application port (Laravel default is 8000)
EXPOSE 8000

# Command to run Laravel's built-in server
#CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
CMD php artisan serve --host=0.0.0.0 --port=8000 & npm run dev -- --host
