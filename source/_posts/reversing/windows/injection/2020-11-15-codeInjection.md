---
title: Code Injection
date: 2020-11-15 16:14:10
tags:
- Code Injection
category:
- Reversing
---


## Code 인젝션

![Code Injection](/img/codeInjection.PNG)
대상 프로세스에 독립 실행 코드를 삽입한 후 실행하는 방법 , 별도의 dll이 필요하지 않는다. 하지만 코드만 인젝셔하는 기법으로 데이터를 따로 인젝션해줘야한다.

### Code Injection 

- 스레드 인자 선언 : LoadLibrary + GetProcAddress + Data
```c++
typedef struct _THREAD_PARAM
{
    FARPROC pFunc[2];
    char szBuf[2][128];
} THREAD_PARAM, *PTHREAD_PARAM
```
pFunc[0] : LoadLibrary함수의 주소
pFunc[1] : GetProcAddress함수의 주소
szBuf[0] : 실행할 함수의 dll 또는 실행할 코드
szBuf[1] : 실행할 함수 또는 실행할 코드

- 함수 포인터 선언 : 인젝션에 사용할 함수 포인터 원형 선언

```c++
typedef HMODULE(WINAPI *PFLOADLIBRARYA) (LPCTSTR lpLibFileName);
typedef FARPROC(WINAPI *PFGETPROCADDRESS) (HMODULE hModule, LPCTSTR lpProcName);
//자신이 실행할 함수 포인터 선언
```

- 데이터 영역 인젝션

```c++
pRemoteBuf[0] = VirtualAllocEx(hProcess,NULL,dwSize,MEM_COMMIT,PAGE_READWRITE);
WriteProcessMemory(hProcess,pRemoteBuf[0],(LPVOID)&param,dwSize,NULL);
```
param : 데이터 영역, 구조체

- 코드 영역 인젝션

```c++
dwSize = (DWORD)InjectCode - (DWORD)ThreadProc
pRemoteBuf[1] = VirtualAllocEx(hProcess,NULL,dwSize,MEM_COMMIT,PAGE_EXECUTE_READWRITE);
WriteProcessMemory(hProcess,pRemoteBuf[1],(LPVOID)ThreadProc,dwSize,NULL);
```
dwSize는 프로그램은 위에서 아래로 실행 되기 때문에 ThreadProc 코드가 InjectCode 코드보다 앞에 있으면 `ThreadProc 시작주소 - InjectCode 시작주소`로 ThreadProc의 크기를 알 수 있다.
데이터 영역은 실행 권한이 필요없지만 코드 부분은 실행 권한이 필요하므로 `PAGE_EXECUTE_READWRITE`가 필요하다
```c++
ThreadProc() { // InjectCode Address - ThreadProc Address = ThreadProc Size

}

InjectCode() {

}
```

- 원격 스레드 실행
```c++
hThread = CreateRemoteThread(hProcess,NULL,0,(LPTHREAD_START_ROUTINE)pRemoteBuf[1],pRemoteBuf[0],0,NULL);
```
pRemoteBuf[0] : THREAD_PARAM , 데이터 부분
pRemoteBuf[1] : 코드 부분

- 코드 부분

```c++
DWORD WINAPI ThreadProc(LPVOID lParam){
    PTHREAD_PARAM pParam = (PTHREAD_PARAM)lParam;
    hMod = ((PFLOADLIBRARYA)pParam -> pFunc[0],(pParam->szBuf[0]);
    pFunc = (FARPROC)((PFGETPROCADDRESS)pParam->pFunc[1])(hMod,pParam->szBuf[1]);
    (*pFunc)() // 함수 포인터 실행
}
```

hMod는 `LoadLibrary(실행할 함수를 가지고 있는 DLL)`를 뜻하고, pFunc은 `GetProcAddress(실행 함수)`를 뜻한다.


