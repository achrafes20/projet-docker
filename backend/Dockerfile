FROM php:8.2-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd zip

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www

# Copy composer files first (optimize Docker cache)
COPY composer.json composer.lock ./

# Install dependencies (without scripts)
RUN composer install --no-scripts --no-autoloader

# Copy all files
COPY . .

# Now run the rest of composer install
RUN composer install

# Generate key
RUN php artisan key:generate

# Permissions
RUN chown -R www-data:www-data /var/www/storage