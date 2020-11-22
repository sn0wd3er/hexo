---
title: Import Binding
date: 2020-11-17 02:18:57
tags:
- Import Binding
category:
- Windows
---

## Import Bounding

프로그램 링크 시 함수의 주소를 해석하고 IAT에 삽입하는 과정을 의미, IMAGE_IMPORT_DESCRIPTOR의 TimeStamp 값이 -1인 경우에 사용한다.

### Pre Binding

로딩 시간에 IAT를 완성하지 않고 링킹 시 IAT를 미리 완성하는 기능 다시말해 미리 IAT를 완성해 놓고 Loader에 그대로 전해주어 바로 로딩할 수 있게 미리 준비하는 방법이다.
하지만 API의 주소가 IAT와 다를 수 있다. 메모리에 올라와 있던 DLL의 TimeDateStamp가 최신이면 IAT를 최신 껄로 덮어 쓴다. IAT구조체에 TimeDateStamp가 -1이면 Bounding을 한 것이다.


### 지연 로드

Pre Binding과 반대로 DLL을 사용하기 전까지 라이브러리를 메모리에 로드하지 않는다. GetProcAddress를 사용해서 DLL 사용 트리거되면 주소를 가져와서 로드해준다. 



