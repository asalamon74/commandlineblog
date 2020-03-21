---
layout: post
title: 'Több avi összefűzése'
permalink: /2010/02/27/tobb_avi_osszefuzese
post_id: 1734760
categories: 
- avi
- mencoder
- transcode
---

Több avi fájlt ( azonos felbontás, kódolás,... ) igen könnyen egymás után kapcsolhatunk újrakonvertálás nélkül az 
```
avimerge
```
 paranccsal ( a 
[transcode](http://tcforge.berlios.de/) programcsomag része ): 
```
avimerge -o nagy.avi -i kis1.avi kis2.avi kis3.avi
``` 
Ha inkább 
[mencoder](http://www.mplayerhq.hu/)t szeretnénk használni, akkor a következő parancsot használhatjuk: 
```
mencoder -ovc copy -oac copy -o nagy.avi kis1.avi kis2.avi kis3.avi
``` 
  
 