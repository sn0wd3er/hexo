---
title: 비휘발성 데이터 수집
date: 2020-11-15 13:56:47
tags:
- Data Collecction
category:
- Forensics
---

## 비휘발성 데이터 수집

### 네트워크 관련 파일
 - Windows\system32\drivers\etc\hosts : 초기 DNS정보르 보관하는 File
 - Windows\system32\drivers\etc\networks : loopback 기본정보
 - Windows\system32\drivers\etc\lmhost : NetBios에서 사용

### 프리패치 파일

 - %systemroot%\Prefetch : 수행되었던 프로그램을 알 수 있다.

### 이벤트 뷰어 로그
 - 컴퓨터 관리 > 이벤트 뷰어

### Systeminternals
 - pslist
 - Listdlls
 - AutoRuns

