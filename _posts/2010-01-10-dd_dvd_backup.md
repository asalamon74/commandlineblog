---
layout: post
title: 'dd (dvd backup)'
permalink: https://commandline.blog.hu/2010/01/10/dd_dvd_backup
post_id: 1658999
categories: 
- dvd
- backup
- iso
- dd
---

Ha szeretnénk egy DVD-ről biztonsági másolatot készíteni, és tényleg csak ennyire van szükségünk (vagyis nem akarjuk eltávolítani a másolásvédelmet vagy átkonvertálni a DVD-t valami más formátumra), akkor nincs szükségünk semmilyen különleges programra, a 
[dd](http://en.wikipedia.org/wiki/Dd_%28Unix%29) programmal egyszerűen elmenthetjük az iso fájlt:

```
dd if=/dev/sr0 of=lemez.iso
```

A 
```
/dev/sr0
```
 helyett persze a saját DVD meghajtónk címét kell írnunk.

 