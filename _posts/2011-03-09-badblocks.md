---
layout: post
title: 'badblocks'
permalink: /2011/03/09/badblocks
post_id: 2717506
categories: 
- merevlemez
- hdd
- badblocks
- e2fsprogs
---

Merevlemezünk esetleges hibás területeit találhatjuk meg a 
[badblocks](http://en.wikipedia.org/wiki/Badblocks) program (
[e2fsprogs](http://e2fsprogs.sourceforge.net/) csomag része) segítségével. 
Alapesetben csak olvasás segítségével próbálja felderíteni a hibákat: 
```
badblocks -v /dev/sdb1
``` 
Van olyan üzemmódja is, amikor írás-olvasás segítségével ellenőrzi a merevlemezt, de igyekszik nem letörölni a merevlemez tartalmát: 
```
badblocks -v -n /dev/sdb1
``` 
Végül pedig van olyan üzemmódja is, amikor az ellenőrzés során nem ügyel a merevlemez tartalmának megőrzésére: 
```
badblocks -v -w /dev/sdb1
``` 
Természetesen mielőtt nekiállunk ellenőrizni a merevlemezt, mindenképpen készítsünk biztonsági másolatot fontos adatainkról! (Nemcsak akkor ha 
```
-w
```
 kapcsolót használjuk, hanem mindig) 
```
/dev/sdb1
```
-et se felejtse el senki átírni a megfelelő címre. 
Ha minden jól megy, valami ilyen eredményt kapunk (
```
-n
```
 kapcsolóval): 
```
Checking for bad blocks in non-destructive read-write mode
 From block 0 to 244195007
 Testing with random pattern: Pass completed, 0 bad blocks found.
```
  