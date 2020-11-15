---
title: 임계 영역과 뮤텍스
date: 2020-11-14 16:53:07
Category:
- Windows
tags:
- Critical Section
- Mutex
---
## 임계 영역(Critical Section)

임계 영역은 같은 프로세스 내부의 스레드 동기화를 처리한다. 한 번에 하나의 스레드만 진입 가능하다. CRITICAL_SECTION 구조체를 사용하여 메모리를 할당한다.

### 임계 영역 함수

- 임계 영역 초기화 : InitializeCriticalSection, InitializeCriticalSectionAndSpinCount
- 임계 영역 사용 : EnterCriticalSection, TryEnterCriticalSection(blocking X), LeaveCriticalSection

## 뮤텍스(Mutex)

뮤텍스는 커널 모드 동기화 오브젝트이다.

### 임계 영역 함수

- 생성 : CreateMutex
- 소유권 획득 : OpenMutex
- 소유권 해제 : ReleaseMutex

### WinDBG 명령어
!cs : 임계 영역 정보 , 해당 임계 영역으로 이동 후 실행해야함

