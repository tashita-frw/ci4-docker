# CodeIgniter4 tutorial  

## 環境構築  

1.GitHub からクローンする
```
git clone git@github.com:tashita-frw/ci4-docker
```  

2.DockerDesktopアプリを立ち上げる  

3.プロジェクト直下に移動し、以下のコマンドを実行する  
```
cd ci4-docker
```
```
docker-compose up -d --build
```

4.dbコンテナに入り、mysqlで下記クエリを実行
```
docker-compose exec db bash
```
```
mysql -u root -p
```
※passwordは、docker-compose.ymlファイル参照
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
