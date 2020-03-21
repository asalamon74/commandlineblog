---
layout: post
title: 'mkv fejezetek'
permalink: https://commandline.blog.hu/2012/11/30/mkv_fejezetek
post_id: 4938959
categories: 
- mkv
- matroska
- mkvmerge
- mkvtoolnix
---

Ha egy meglévő mkv fájlhoz szeretnénk beállítani a fejezethatárokat, akkor egy meglehetősen egyszerű szövegfájlban (chap.txt) kell megadnunk a fejezetek határait:

```
CHAPTER01=00:00:00.000
CHAPTER01NAME=Első
CHAPTER02=00:02:30.000
CHAPTER02NAME=Második
CHAPTER03=00:02:42.300
CHAPTER03NAME=Harmadik
```

eztán a következő paranccsal tudjuk az új mkv-t elkészíteni:

```
mkvmerge input.mkv --chapters chap.txt -o output.mkv
```