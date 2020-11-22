---
title: Kali에서 도커 설치 및 로그(워드프레스)
date: 2020-11-19 17:34:41
tags:
- Docker Wordpress
- Docker
category:
- ETC
---

## 설치

sudo apt-get update
sudo apt install docker.io
sudo service docker start

### Docker 간단 Command

- `docker search []` : 이미지 찾기
- `docker pull []` : 이미지 설치
- `docker run -p [호스트에서 사용할 PORT]:[Container PORT] []` : 도커 실행

### Docker 쉘 동작


- `sudo docker container run -i -t --name [Name] [Image] /bin/bash`
- `sudo docker exec -i -t [Image] /bin/sh`

### Docker Container 중지

- `docker stop [Image]`

### Docker Image 제거

- `docker rm`

## Install Wordpress

#### MySQL
- `docker run -d --name mysql -v mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=wordpress -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wordpress -e MYSQL_PASSWORD=wordpress mysql:5.7`

#### WordPress
- `docker run -d --name wordpress -v wordpress:/var/www/html --link mysql:mysql -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_PASSWORD=wordpress -p 80:80 wordpress:latest`

## Logs

- `sudo docker inspect [image]` : 도커 설정 보기
- `sudo docker logs [Image]`


