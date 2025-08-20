# 1. ベースイメージ
FROM php:8.1-apache

# 2. apt パッケージリスト更新
RUN apt-get update

# 3. ICU（intl）用ヘッダをインストール
RUN apt-get install -y libicu-dev

# 4. intl 拡張モジュールをインストール
RUN docker-php-ext-install intl

# 5. XML 用ヘッダをインストール
RUN apt-get install -y libxml2-dev

# 6. XML 拡張モジュールをインストール
RUN docker-php-ext-install xml

# 7準備. oniguruma ヘッダ（mbstring の必須）
RUN apt-get install -y libonig-dev

# 7. mbstring インストール
RUN docker-php-ext-install mbstring

# 8. ZIP 用ヘッダをインストール
RUN apt-get install -y libzip-dev

# 9. ZIP モジュールをインストール
RUN docker-php-ext-install zip

# 10. MySQL ネイティブドライバをインストール
RUN docker-php-ext-install pdo_mysql

# 10追加 MySQLiをインストール
RUN docker-php-ext-install mysqli

# 11. Apache の rewrite モジュールを有効化
RUN a2enmod rewrite

# グローバルにサーバ名を設定（警告抑制）
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# 12. Composer をグローバルに配置
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 13. 作業ディレクトリを設定
WORKDIR /var/www/html

# 14. Apache DocumentRoot を public ディレクトリに変更
RUN sed -i 's|DocumentRoot /var/www/html|DocumentRoot /var/www/html/src/public|g' /etc/apache2/sites-available/000-default.conf

# 15. 不要なキャッシュを削除してイメージを軽量化
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
