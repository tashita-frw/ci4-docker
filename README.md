# CodeIgniter4 tutorial  

## 環境構築  

1.GitHub からクローンする
```
git clone git@github.com:tashita-frw/ci4-docker
```  

2.DockerDesktopアプリを立ち上げる  

3.プロジェクト直下に移動し、.envファイルを設定する。
```
cd ci4-docker
```
```
cp .env.example .env
```
.envを設定(例)
```
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=ci4db
MYSQL_USER=ci4user
MYSQL_PASSWORD=ci4pass
```
その後下記コマンドを実行。
```
docker-compose up -d --build
```
4.appコンテナに入り、composerのインストールとwritableの必要なフォルダを作成
```
docker-compose exec app bash
```
```
cd /var/www/html/src
```
```
composer install
```
```
mkdir -p /var/www/html/src/writable/{cache,logs,session,uploads}
```
```
chown -R www-data:www-data /var/www/html/src/writable
```
```
chmod -R 775 /var/www/html/src/writable
```
codeigniterの環境変数の設定

```
cp env .env
```
```
chmod -R 775 /var/www/html/src/.env
```
環境変数を設定(例)
```
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=ci4db
MYSQL_USER=ci4user
MYSQL_PASSWORD=ci4pass
```
5.dbコンテナに入り、mysqlで下記クエリを実行
```
docker-compose exec db bash
```
```
mysql -u root -p
```
※passwordは、プロジェクト直下の.env参照
```
USE ci4db
```
```
CREATE TABLE news (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    title VARCHAR(128) NOT NULL,
    slug VARCHAR(128) NOT NULL,
    body TEXT NOT NULL,
    PRIMARY KEY (id),
    UNIQUE slug (slug)
);
```
```
INSERT INTO news VALUES
(1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
(2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.'),
(3,'Caffeination, Yes!','caffeination-yes','World\'s largest coffee shop open onsite nested coffee shop for staff only.');
```

# URL  
・home画面:http:http://localhost:8080/home  
・about画面:http:http://localhost:8080/about  
・news画面:http://localhost:8080/news  
・create画面:http://localhost:8080/news/new    
