---
layout: post
title: 'mediainfo - DV dátum'
permalink: /2014/06/09/mediainfo_dv_datum
post_id: 6289550
categories: 
- dv
- mediainfo
---

Találtam pár régi 
[DV](http://en.wikipedia.org/wiki/DV) fájlt a gépemen, és kíváncsi voltam mikor készültek a felvételek. Emlékeztem arra, hogy a régien használt kino editor kiírta a felvétel dátumát is, vagyis valahol megvan az információ a fájlban.

Némi kutatás után rátaláltam a 
[mediainfo](http://mediaarea.net/en/MediaInfo) projectre, ami sokféle média fájlból képes információt kiolvasni:

```
$ mediainfo kazetta1002.dv | grep -i date 
Recorded date : 2003-12-22 15:49:09.000
```