FROM php:8.4-fpm-alpine

# Instala dependências do sistema
RUN apk add --no-cache \
    bash \
    curl \
    git \
    zip \
    unzip \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    libzip-dev \
    libxml2-dev \
    oniguruma-dev \
    postgresql-dev \
    autoconf \
    gcc \
    g++ \
    make \
    npm \
    nodejs

# Instala extensões PHP
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) pdo_pgsql mbstring zip gd xml bcmath

# Instala Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Instala o Laravel Installer globalmente
RUN composer global require laravel/installer

# Adiciona o diretório de binários globais do Composer ao PATH
ENV PATH="/root/.composer/vendor/bin:${PATH}"

# Define diretório de trabalho (vai usar volume da máquina)
WORKDIR /var/www