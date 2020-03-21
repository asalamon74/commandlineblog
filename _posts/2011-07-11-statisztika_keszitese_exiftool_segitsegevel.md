---
layout: post
title: 'Statisztika készítése exiftool segítségével'
permalink: https://commandline.blog.hu/2011/07/11/statisztika_keszitese_exiftool_segitsegevel
post_id: 3054174
categories: 
- exif
- exiftool
- digitális_fénykép
---

Egy digitális fénykép nagyon sok információt tárol a készítés körülményeiről, melyekből érdekes statisztikákat készíthetünk 
[exiftool](http://commandline.blog.hu/2010/05/14/exiftool) segítségével. A következő egyszerű példa a használt gyújtótávolság (fókuszhossz) alapján vizsgálja meg a készített képeket: 
```
exiftool -T -FocalLengthIn35mmFormat *.dng | cut -f 1 -d ' ' | sort | uniq -c
``` 
Az eredmény egy táblázat, ahol az első szám a gyakoriságot, a második a gyújtótávolságot (pontosabban a 35mm-re átkonvertált értéket) tartalmazza: 
```
     35 27
       8 30
       6 31
       2 34
       5 36
       3 39
      10 42
       5 46
       4 49
       1 52
       5 57
       7 60
       3 64
       2 72
       6 75
      22 82
```
  Hasonló módszerrel készíthetünk statisztikát pl. a rekeszről, a záridőről, az objektívről...