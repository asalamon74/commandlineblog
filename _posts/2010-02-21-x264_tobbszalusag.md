---
layout: post
title: 'x264 többszálúság'
permalink: /2010/02/21/x264_tobbszalusag
post_id: 1701560
categories: 
- ffmpeg
- smp
- x264
- transcode
- h264
---

Manapság az egyik leginkább időigényes feladat amit egy átlagszámítógép végez, a videókonvertálás. Különösen fontos, hogy többmagos processzorunk összes magja ki legyen használva ilyenkor. Az egyik legismertebb linuxos h264 kódoló, az 
[x264](http://www.videolan.org/developers/x264.html) szerencsére támogatja a többszálúságot. 
Attól függően, milyen módon használjuk, eltérő a többszálúság bekapcsolásának módja. Én transcode-ot használok ffmpeg export modullal ( 
[itt](/2010/02/15/mjpeg_konvertalasa) egy példa ), ebben az esetben az 
```
ffmpeg.cfg
```
 fájlban adhatjuk meg a szálak számát: 
```
[h264]
 threads=2
``` 
Elvileg a 
```
threads=auto
```
 beállításával automatikusan választja ki x264 a processzor alapján a szálak számát, nekem ez nem működött.  