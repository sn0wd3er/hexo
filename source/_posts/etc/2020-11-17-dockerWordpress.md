---
title: 워드프레스 설치(도커)
date: 2020-11-17 15:22:22
tags:
- Install Wordpress
category:
- ETC
---

## 설치

- MySQL

```cmd
docker run -d --name mysql -v mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=wordpress -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress -e MYSQL_PASSWORD=wordpress mysql:5.7

```

- Wordpress

```cmd
docker run -d --name wordpress -v wordpress:/var/www/html --link mysql:mysql -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_PASSWORD=wordpress -p 80:80 wordpress:latest
```


