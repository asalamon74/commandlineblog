---
layout: post
title: 'dvdauthor'
permalink: /2010/03/05/dvdauthor
post_id: 1755134
categories: 
- dvd
- transcode
- mjpegtools
- genisoimage
- dvdauthor
---

Ha Linux alatt DVD-t szeretnénk készíteni, akkor a 
[dvdauthor](http://dvdauthor.sourceforge.net/) program szinte megkerülhetetlen. Igen sok grafikus interfésszel rendelkező linuxos program is erre épül. Leginkább XML nyelven paraméterezhetjük dvdauthort, de az alapvetőbb dolgokat XML nélkül is megvalósíthatjuk. A következő példa is ilyen. 
Adott 
```
mozi.vob
```
 fájl ( mondjuk egyik DVD-nkről ) és ebből szeretnénk DVD-t írni, menü nélkül. Az egyszerűség kedvéért feltételezzük, hogy a videó mpeg2 ( ez szinte mindig igaz ), az audió pedig ac3 ( ez is igen gyakori ). 
```
tcextract -i mozi.vob -t vob -x mpeg2 > mozi.m2v
 tcextract -i mozi.vob -t vob -x ac3 > mozi.ac3 
 mplex -f 8 -o mozi.mpg mozi.m2v mozi.ac3
 dvdauthor -o dvddir -t mozi.mpg 
 dvdauthor -o dvddir -T
 genisoimage -o mozi.iso -dvd-video dvddir/
``` 
Először 
```
tcextract
```
-tal ( 
[transcode](http://tcforge.berlios.de/) csomag ) szétválasztjuk a vob videó és audió streamjét, majd 
```
mplex
```
 ( 
[mjpegtools](http://mjpeg.sourceforge.net/) csomag ) segítségével újra összefűzzük. ( Ez elsőre feleslegesnek tűnik, de szükség van rá ).Ezután a frissen gyártott 
```
mozi.mpg
```
 fájlt új title-ként hozzáadjuk a dvd-hez ( 
```
-t
```
 kapcsoló ). Ha van elég hely, akár több title-t is hozzáadhatunk. Miután hozzáadtuk az összeset, tartalomjegyzéket is kell generáltatnunk ( 
```
-T
```
 kapcsoló ).Végül a dvdauthor által készített 
```
dvddir
```
 alkönyvtárból 
```
iso
```
 fájlt gyártunk, amit már kiírhatunk a lemezre.