---
title: File Upload Attack
date: 2020-11-17 16:06:48
tags:
- File Upload Attack
category:
- Web
---

## File Upload 취약점

웹 쉘등 악의적인 파일을 웹 서버에 업로드하여 침투하는 공격, 보통 확장자를 검증이 미약하여 업로드가 된다.


### 파일 업로드 취약점 조건

1. 업로드할 확장자가 허용되어야 한다.
1. 업로드한 파일의 절대 경로를 알아야 한다.
1. 업로드한 파일의 실행권한이 있어야 한다.

### 웹 서버를 시작으로 근접 네트워크 침투

데이터베이스에 직접 공격을 할 수 없기 때문에, 웹 서버로 침투 후 내부 시스템의 정보를 획득 -> 내부 포탈 서버, 로그 서버 등 내부 시스템 대상으로 포트포워딩, 터널링 기법을 이용

#### 포트 포워딩, 터널링

포트 포워딩은 포트 끼리 연결을 시켜주는 거다. 공격자는 내부망에 침투할 수 없으므로 웹 서버(WAS)를 통하여 내부망으로 침투를 해야한다. 웹 서버에 침투 후 내부망 서버나 PC등에 정보를 수집 후 취약한 서비스가 열려있거나 하면 웹 서버의 포트와 공격자 포트랑 연결 시킨 후 웹 서버와 내부망의 취약한 서비스 포트와 연결 시켜 하나의 길을 뚫어준다 생각하면 된다.

- 취약한 포트 80
- 웹 서버 5555
- 공격자 4444

공격자(4444) <----> WAS(5555) <----> 내부망 취약 서비스 포트(80)


`meterpreter> protfwd add -l [locahost 포트] -p [포워딩할 대상 포트] -r [포워딩할 대상IP]`


#### BurpSuite 

Burpsuite의 Intruder나 Repeater로 우회되는 확장자를 BruteForce로 찾는 방법도 있다.

#### Bypass

1. 자바스크립트 우회
1. 블랙리스트 방식 우회
1. PHP - php3 , php5 , phtml..
1. jsp - jsp , JSP , JsP , js%70
1. asp(IIS) - asp , aspx , asa , cer , asx (Windows같은 경우는 대소문자 구분안하지만 Linux환경은 대소문자를 구분함)
1. 화이트 리스트 방식 우회 - jpg,png,doc,pdf.. , 화이트 리스트는 웹 자체의 취약점을 이용해서 우회해야한다.
1. IIS웹 서버 경우 shell.exe;jpg로 확장자를 우회한 후 파일을 올리게 되면 IIS의 취약점인 왼쪽에서 오른쪽으로 값을 읽어나가기 때문에 shell.exe;까지만 보고 shell.exe를 실행한다는 취약점이 있다 

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Upload%20Insecure%20Files


