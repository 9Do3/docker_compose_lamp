# php7.4とapacheのイメージを指定
FROM php:7.4.9-apache

# ドキュメントルート用の環境変数設定
ENV APACHE_DOCUMENT_ROOT /var/www/html

# ドキュメントルート設定
RUN if [ ! -d ${APACHE_DOCUMENT_ROOT} ]; then mkdir -p ${APACHE_DOCUMENT_ROOT} ; fi
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# 拡張機能インストール
RUN apt-get update && apt-get install -y \
        curl apt-utils apt-transport-https debconf-utils gcc build-essential \
        zlib1g-dev git gnupg2 unzip libfreetype6-dev libjpeg62-turbo-dev \
        libpng-dev libzip-dev libicu-dev vim git ssl-cert \
        && docker-php-ext-install -j$(nproc) zip gd mysqli pdo_mysql opcache intl \
        && rm -rf /var/lib/apt/lists/*

# 拡張機能インストール（postgres用）
RUN apt-get update && apt-get install -y libpq-dev \
        && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
        && docker-php-ext-install -j$(nproc) pgsql pdo_pgsql \
        && rm -rf /var/lib/apt/lists/*

# ロケール設定
RUN apt-get update && apt-get install -y locales \
        && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
        && locale-gen

# Apache2モジュール有効化
RUN a2enmod rewrite
RUN a2enmod headers

# SSL有効化
RUN a2enmod ssl
RUN a2ensite default-ssl
EXPOSE 443

# composerインストール
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/bin/composer

# イメージに付属のphp.ini-development（開発用）をphp.iniとして配置
RUN cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"