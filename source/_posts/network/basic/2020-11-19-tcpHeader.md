---
title: TCP
date: 2020-11-19 14:01:44
tags:
- TCP
category:
- Network
---

## TCP

![TCP Header](/img/tcpheader.PNG)

헤더의 크기는 최소 20byte이지만 옵션으로 40byte를 추가하여 총 60byte가 될 수 있다.

### Header

|Format|설명|
|:---:|:---|
|Port Number|송신 포트와 수신 포트 번호|
|Sequence Number|Syn이 Random값으로 초기값이다,Syn-Ack 초기값에 1을 더한 값|
|Ack Number|다음 세그먼트에 실릴 것으로 예상된 데이터의 순차 번호|
|N Flag|ECN의 유효성 표시 신호|
|C Flag|폭주 윈도 감소|
|E Flag|Syn=1인 경우 ECN을 지원여부를 알림, SYN=0인 경우 폭주 발생 여부를 송신자에게 알림|
|U Flag| 긴급 필드 포인터의 유효 여부를 알림|
|A Flag| ACK 필드의 유효 여부를 알림|
|P Flag| 수신 측이 버퍼 데이터를 가져가기를 요구함|
|R Flag| TCP 연결 Handshake를 취소|
|S Flag| 시퀀스 번호 동기화|
|F Flag| TCP 연결 종료를 요구|
|Window Size| 수신자가 현재 가진 데이터 버퍼의 크기|
|Checksum| 페이로드에 대한 Checksum을 표시|
|Urgen Pointer| URG Flag가 1일 때 긴급 데이터의 마지막 바이트의 오프셋을 표시한다|

- Congestion : 폭주를 의미

### TCP HandShake

![HandShake](/img/tcphandshake.PNG)

- Syn: 임의의 랜덤 값
- Syn+Ack : 전 Ack값 + 다음에 받을 값
- Ack : Ack으로 받은 값 + 다음에 받을 값



