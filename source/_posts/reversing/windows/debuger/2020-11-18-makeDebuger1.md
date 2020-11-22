---
title: Debuger 제작1
date: 2020-11-18 01:21:34
tags:
- Debuger 제작
category:
- Reversing
---

## 디버깅 API

|API|설명|
|:---:|:---|
|CreateProcess()|새로운 프로세스와 그 프로세스의 주 스레드를 생성|
|WaitForDebugEvent()|디버깅 중 프로세스에서 이벤트가 발생하는 것을 기다리는 함수|
|ContinueDebugEvent()|디버그 이벤트로 인해 정지 상태에 있는 스레드를 다시 실행해주는 함수|

```c++
BOOL WINAPI CreateProcess{
	_In_opt_ LPCTSTR lpApplicationName // 실행할 애플리케이션 이름
	_Inout_opt_ LPTSTR lpCommandLine // 명령어 인자
	_In_ DWORD dwCreationFlags // 디버깅 목적 명시
	_In_ LPSTARTUPINFO lpStartupInfo // 프로세스 실행 형식에 대한 정보
	_Out_ LPPROCESS_INFORMATION lpProcessInformation // 프로세스 실행 결과를 확인하기 위한 정보
}
```

Debuger를 만들 때 가장 중요한 정보이다. 불필요한 인자는 생략했으니 공식 문서 참고


## 디버그 이벤트 핸들러 

디버기에서 이벤트 발생 시 이벤트를 처리할 핸드러를 구현해야 한다.

|이벤트 코드|코드 값|설명|
|:---:|:---:|:---|
|0x1|EXCEPTION_DEBUG_EVENT|예외 디버깅 이벤트|
|0x2|CREATE_THREAD_DEBUG_EVENT|스레드 생성 디버깅 이벤트|
|0x3|CREATE_PROCESS_DEBUG_EVENT|프로세스 생성 디버깅 이벤트|
|0X4|EXIT_THREAD_DEBUG_EVENT|스레드 종료 디버깅 이벤트|
|0x5|EXIT_PROCESS_DEBUG_EVENT|프로세스 종료 디버깅 이벤트|
|0x6|LOAD_DLL_DEBUG_EVENT|DLL 로드 디버깅 이벤트|
|0x7|UNLOAD_DLL_DEBUG_EVENT|DLL 언로드 디버깅 이벤트|
|0x8|OUTPUT_DEBUG_STRING_EVENT|디버깅 문자열 출력 이벤트|
|0x9|RIP_EVENT|RIP 디버깅 이벤트(시스템 디버깅 에러)|

## 디버거 이벤트 출력 소스 코드

```c++
#include <stdio.h>
#include <tchar.h>
#include <windows.h>


void PrintEvent(DEBUG_EVENT d_event) {
	switch (d_event.dwDebugEventCode) {
	case EXCEPTION_DEBUG_EVENT:
		printf("Except debug event\n");
		break;
	case CREATE_THREAD_DEBUG_EVENT:
		printf("Create thread debug event\n");
		break;
	case CREATE_PROCESS_DEBUG_EVENT:
		printf("Create process debug event\n");
		break;
	case EXIT_THREAD_DEBUG_EVENT:
		printf("Exit thread debug event\n");
		break;
	case EXIT_PROCESS_DEBUG_EVENT:
		printf("Exit process debug event\n");
		break;
	case LOAD_DLL_DEBUG_EVENT:
		printf("Load dll debug event\n");
		break;
	case UNLOAD_DLL_DEBUG_EVENT:
		printf("Unload dll debug event\n");
		break;
	case OUTPUT_DEBUG_STRING_EVENT:
		printf("Output debug string event\n");
		break;
	case RIP_EVENT:
		printf("Rip event\n");
		break;
	default:
		printf("It`s Default");
	}
	printf("Event Code: %d\n", d_event.dwDebugEventCode);
}


int _tmain(int argc, TCHAR* argv[]) {
	
	STARTUPINFO si;
	PROCESS_INFORMATION pi;
	ZeroMemory(&si, sizeof(si)); //initialize 0
	ZeroMemory(&pi, sizeof(pi));
	si.cb = sizeof(si); //si size

	DEBUG_EVENT d_event = { 0, }; //Debug Event Structure

	WCHAR szCmdLine[] = L"C:\\windows\\system32\\notepad.exe"; //Path

	if (!CreateProcess(NULL, szCmdLine, NULL, NULL, FALSE, DEBUG_PROCESS, NULL, NULL, &si, &pi)) {
		printf("CreateProcess Error!!, %d\n", GetLastError());
		return -1;
	}//Create Debuger
	
	while (true) {
		if (!WaitForDebugEvent(&d_event, INFINITE)) { //Catch Debug Event
			break;
		}

		//handle event
		PrintEvent(d_event);

		ContinueDebugEvent(d_event.dwProcessId, d_event.dwThreadId, DBG_CONTINUE); //Debug Continue
	}

	
	return 0;
}
```
