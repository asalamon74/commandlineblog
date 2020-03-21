---
layout: post
title: 'merevlemez törlése'
permalink: https://commandline.blog.hu/2011/03/06/merevlemez_torlese
post_id: 2713534
categories: 
- merevlemez
- hdd
- dd
- shred
---

Mielőtt eladjuk egy régi merevlemezünket, mindenképpen érdemes a  tartalmát teljesen törölni (hacsak nem szeretnénk, hogy a vevő  hozzáférjen a régi fájlainkhoz). 
Legegyszerűbb megoldás a dd használata: 
```
dd if=/dev/urandom of=/dev/sdb bs=1M 
dd if=/dev/zero of=/dev/sdb bs=1M
```Az első parancs véletlenszerű adattal, a második  csupa nullával írja tele a merevlemezt.  
Ha ennél is többre vágyunk, akkor a 
[shred](http://linux.about.com/library/cmd/blcmdl1_shred.htm)-et érdemes használni: 
```
shred -vfz /dev/sdb
``` 
Azutasítás hatására háromszor ( ez az alapértelmezett érték, de 
```
-n
```
 kapcsolóval eltérő értéket is megadhatunk ) véletlenszerű adatokkal írjuk tele a merevlemezt, majd ezután (
```
-z
```
 kapcsoló) csupa nullával írjuk tele. 
/dev/sdb-t ne felejtse el senki átírni! 