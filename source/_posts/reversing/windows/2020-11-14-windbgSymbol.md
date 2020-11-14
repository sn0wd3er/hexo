---
title: Windbg 심볼 설정
date: 2020-11-14 16:13:32
category:
- Reversing
- Windows
tags:
- Windbg
---

## 명령어

- .sympath srv\*c:\\Symbols\*http//msdl.Microsoft.com/download/symbols
- .sympath srv\*\\\\myserver\\mysymbols\*c:\Symbols\*http//msdl.Microsoft.com/download/symbols
- .reload
- .symfix c:\symbols
- .reload
