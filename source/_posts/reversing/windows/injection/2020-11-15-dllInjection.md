---
title: DLL Injection
date: 2020-11-15 16:04:31
tags:
- DLL Injection
category:
- Reversing
---


## Injection 기법

실행 중인 다른 프로세스에 DLL 또는 코드를 강제로 삽입하는 방법, 크게 DLL 인젝션과 Code 인젝션으로 나눈다.


### DLL 인젝션

![Injection](/img/injection.PNG)
DLL 인젝션은 Injector와 DLL 두 개가 필요하다. Injector는 DLL을 삽입하게 해주는 프로그램이고, Injection DLL은 DLL파일로 삽입된 후에 실행할 프로그램이다.
실행 순서는 프로세스 핸들 -> 대상 프로새스 공간 확보 -> DLL이름 쓰기 -> 라이브러리 로드 -> 원격 스레드 실행 순으로 실행된다.'


#### DLL Injector

- OpenProcess() : 해당 프로세스 오브젝트에 대한 모든 권한을 획득
`hprocess = OpenProcess(PROCESS_ALL_ACCESS, FALSE, dwPID)`
- VirtualAllocEx() : 공간 확보
`pRemoteBuf = VirtualAllocEx(hProcess,NULL,dwBufSize,MEM_COMMIT,PAGE_READWRITE)`
dwBufSize : (DWORD)(_tcslen(szDllPath)+1) * sizeof(TCHAR), 인젝션할 DLL의 경로의 길이(크기)이다.
- WriteProcessMemory() : 인젝션 대상 프로세스에 인젝션 DLL경로 쓰기
`WriteProcessMemroy(hProcess,pRemoteBuf,(LPVOID)szDllName,dwBufSize,NULL)`
- LoadLibrary() API 주소 구하기
```c
hMod = GetModuleHandle("kernel32.dll")
pThreadProc = (LPTHREAD_START_ROUTINE)GetProcAddress(hMod,"LoadLibraryW")
```
GetModuleHandle은 기본적으로 인젝션 대상 프로세스에서 "kernel32.dll"을 불러오기 때문이다.
- 대상 프로세스에서 원격 스레드 실행
`hThread = CreateRemoteThread(hProcess,NULL,0,pThreadProc,pRemoteBuf,0,NULL)`
LoadLibrary()를 쓰면 인젝터 자신 프로세스에서 실행되어지는 것이기 때문에 ThreadProc()으로 실행시켜 인젝션 대상 프로세스의 하위 Thread로 실행 시켜야한다.
- WaitingForSingleObject() : 스레드가 실행될 때 까지 대기

#### DLL

- ThreadProc() : Thread가 수행할 코드
`DWORD WINAPI ThreadProc(LPVOID lParam)`

- BOOL WINAPI DllMain() : Dll의 Main 함수
```c++
BOOL WINAPI DllMain(HINSTANCE hinstDLL,DWORD fdwReason, LPVOID lpvReserved){
    switch(fdReason){
    case DLL_PROCESS_ATTACH:
        // Code
}
```

