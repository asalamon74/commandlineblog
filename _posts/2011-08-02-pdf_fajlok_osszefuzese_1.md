---
layout: post
title: 'pdf fájlok összefűzése'
permalink: /2011/08/02/pdf_fajlok_osszefuzese_1
post_id: 3113586
categories: 
- pdf
- gs
- ghostscript
---

Bár vannak egyszerűbb módok is, ha pdf fájlokat kell összefűzni, legtöbbször a jó öreg 
[ghostscript](http://pages.cs.wisc.edu/~ghost/)et használom, ezzel van a legkevesebb probléma: 
```
gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOUTPUTFILE=egyben.pdf elso.pdf masodik.pdf
```