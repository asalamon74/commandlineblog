---
layout: post
title: 'Több mp4 összefűzése'
permalink: https://commandline.blog.hu/2012/06/29/tobb_mp4_osszefuzese
post_id: 4618528
categories: 
- mp4
- MP4Box
- GPAC
---

Az 
[avi](http://commandline.blog.hu/2010/02/27/tobb_avi_osszefuzese) és 
[mkv](http://commandline.blog.hu/2010/04/02/tobb_matroska_osszefuzese) összefűzéshez hasonlóan most mp4 fájlokat kellett összeragasztanom (újrakódolás nélkül persze). Ehhez 
[MP4Box](http://gpac.wp.mines-telecom.fr/mp4box/) parancsot használtam ( 
[GPAC](http://gpac.wp.mines-telecom.fr/) csomag része ):

```
MP4Box -cat input1.mp4 -cat input2.mp4 output.mp4
```

Kiegészítés:

Nemrég azt tapasztaltam, hogy szerencsésebb ezt a változatot használni:

```
MP4Box -force-cat -cat input1.mp4 -cat input2.mp4 -new output.mp4
```