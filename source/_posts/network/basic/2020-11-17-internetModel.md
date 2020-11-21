---
title: 인터넷 모델
date: 2020-11-17 08:36:44
tags:
- 인터넷 모델
- 인터넷 물리적 구조
category:
- Network
---

## 인터넷 모델

### AS 

AS는 ISP가 운영하는 인터넷 영역으로 여러 IP를 모은 IP 가상의 집합으로 IP 그룹이다.AS마다 번호가 붙고 AS는 BGP프로토콜이나 게이트웨이가 많이 이용한다.


### 인터넷 계층 모델 TCP/IP

![TCP/IP](/img/tcpIP.PNG) 
[^https://en.wikipedia.org/wiki/Internet_protocol_suite]


### 인터넷 물리적 구조

![인터넷 물리적 구조](/img/internetstructure.PNG)


#### Backbone Network

- 빠른 속도로 서브넷을 연결시켜주는 역할을 한다. 주로 Router로 구성

#### Switch 

- PORT : 스위치 내부의 고유 포트번호, 다른 노드와 연결시켜주는 인터페이스이며 MAC Table이랑 포트번호랑 매치시켜 데이터를 전송함. 참고로 PROT는 물리적인 것으로 유선으로 연결되어 있음
- MAC 주소를 사용

#### ROUTER

- 스위치랑 다르게 PORT대신 NIC를 가지고 있고 IP Table과 NIC와 매치시켜 경로를 설정해줌
- IP를 사용


#### HUB

- 포트는 데이터 전송이 있을 때 모든 PORT에 전송한다. 따라서 모든 포트가 충돌영역 및 방송영역이다.

#### BRIDGE

- 둘 이상의 네트워크를 상호 연결해주는 데이터링크 장비
- 충돌 영역을 분할함

#### REPEATER

- 전송 신호를 증폭 시킴 
