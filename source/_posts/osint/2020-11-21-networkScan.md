---
title: Netenum, Netdiscover
date: 2020-11-21 14:59:10
tags:
- Netenum
- Netdiscover
category:
- OSINT
---

## Netenum

Netenum은 네트워크 대역에 있는 호스트들을 스캔해주는 도구이다.

### 설치

```cmd
sudo apt-get update
sudo apt install irpas
```

### 사용법

```cmd
sudo netenum [IP대역] [Time:10] [Verbos:0]
```

## Netdiscover

ARP 프로토콜을 활용하여 네트워크에 연결된 클라이언트를 검색하는 스캐너

### 사용법

```cmd
sudo netdiscover -r [IP 대역]
```


