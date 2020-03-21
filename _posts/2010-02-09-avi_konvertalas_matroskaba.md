---
layout: post
title: 'avi konvertálás matroskába'
permalink: /2010/02/09/avi_konvertalas_matroskaba
post_id: 1688481
categories: 
- avi
- mkv
- matroska
---

Egyre elterjedtebb a 
[matroska](http://www.matroska.org/) konténerformátum, úgy néz ki lassan leváltja a jó öreg 
[avi](http://hu.wikipedia.org/wiki/AVI)-t. Matroska fájlok kezelésében az 
[MKVToolnix](http://www.bunkus.org/videotools/mkvtoolnix/) csomag segít. Az egyik legegyszerűbb feladat egy már létező avi átcsomagolása mkv formátumba (újrakódolás nélkül persze): 
```
mkvmerge -o teszt.mkv teszt.avi
```