# ベースイメージ
FROM php:8.1-apache

# 必要なパッケージとPHP拡張をまとめてインストール
RUN apt-get update && \
  apt-get install -y \
  libicu-dev \
  libxml2-dev \
  libonig-dev \
  libzip-dev && \
  docker-php-ext-install \
  intl \
  xml \
  mbstring \
  zip \
  pdo_mysql \
  mysqli && \
  a2enmod rewrite && \
  echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Composer をグローバルに配置
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 作業ディレクトリと Apache の DocumentRoot を設定
WORKDIR /var/www/html
RUN sed -i 's|DocumentRoot /var/www/html|DocumentRoot /var/www/html/src/public|g' /etc/apache2/sites-available/000-default.conf
