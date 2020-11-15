---
title: 윈도우 정보 수집 기본 명령어
date: 2020-11-15 13:36:08
tags:
- Information Collection
category:
- Forensics
---

## 시스템 정보 수집

### RunAs

권한을 변경하기 위한 명령어(su) 

`runsas /user:administrator notepad`

### 환경 변수

%SystemRoot%, %homedrive%, %Windir%, %Path% ..

`echo %SystemRoot%` : 환경 변수 출력
`set My_Path = "%PATH"` : 현재 세션에 환경 변수 설정
`setx My_Path = "%PATH%;c:\Myfiles" : 시스템 변수에 환경 변수 셜정

### 시스템 정보 확인

- `ver`
- `winver`


### 시스템 서비스, 드라이버, 속성

- `SystemInfo` : 시스템 구성 정보
- `DriverQuery /v /fo list` : 장치 드라이브 정보
- `Sc query` : 서비스 컨트롤러
- `Reg` : 레지스트리
- `Shutdown`
- `Where x.txt`


### 시스템 시간 / 날짜

- `date /t`
- `tile /t`

### 계정 정보 확인

- `whoami /user`
- `whoami /logonid`
- `whoami / priv`
- `whoami /all`

### 시스템 이벤트, 프로세스, 작업 모니터

- `tasklist /fo list /v` : 프로세스 상세 정보
- `tasklist /svc` : 서비스 정보
- `tasklist /m` : DLL 모듈
- `taskkill /pid [PID]` : 프로세스 종료


### net 명렁 계정/그룹

- `set user` : 계정 확인
- `net user` : 계정 확인

### net 명령 정책, 공유

- `net accounts` -> secpol.msc
- `net config`
- `net share` : 공유 폴더

### net 명령 서비스

- `net start dhcp` : dhcp서비스 시작

### arp 캐시

- `arp -a` : 캐시 조회
- `arp -d` : 캐시 초기화
- `arp -s 1.1.1.1 MAC` : 정적 arp 설정

### DNS

- `ipconfig /all`
- `ipconfig /renew, release` - DHCP
- `ipconfig /flushdns, /displaydns`

DNS 조회 순서 : DNS 캐시 -> host -> DNS 서버

### 네트워크

- `netstat` : -anp## , -anop(PID), -anbp(DLL)

### 명령어 이력, 예약된 작업
- `doskey /history`
- `schtasks`
