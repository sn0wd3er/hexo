---
title: Subdomain 검색 방법
date: 2020-11-21 15:38:49
tags:
- Subdomain
category:
- OSINT
---

## Search


### Google

```google
site:google.com -site:www.google.com ~~
```

### DNSdumster

https://dnsdumpster.com/

### Facebook ct

https://developers.facebook.com/tools/ct

### Sublist3r

https://github.com/aboul3la/Sublist3r

#### 사용법

```cmd
python3 sublist3r.py -d google.com
```

### fierce

```cmd
fierce --dns google.com
```
