---
layout: post
title: 'mplayer -vf cropdetect'
permalink: /2012/10/24/mplayer_-vf_cropdetect
post_id: 4864779
categories: 
- mplayer
- crop
- mencoder
---

Kellően el nem ítélhető módon többször találkozhatunk olyan videóval, ahol a megfelelő képarányt a kép tetejére/aljára illesztett fekete csíkkal próbálják garantálni. Külön kellemes, amikor egy eredetileg 16:9 arányú videónál fekete csíkokkal érik el, hogy 4:3 arányú képernyőn arányos legyen, majd amikor ezt egy 16:9 arányú monitoron nézzük, akkor a videólejátszó program automatikusan a bal és jobb oldalra is fekete csíkot tesz, vagyis végeredményben a kép mind a 4 szélén fekete csíkot nézhetünk.

Az ilyen csíkok eltávolítása nem túl nehéz, de persze meg kell határozni, hogy pontosan milyen vastagok is az eltávolítandó csíkok. Az eltávolítandó csíkok automatikus felismeréséhez is ad támogatást 
[mplayer](http://www.mplayerhq.hu/):

```
mplayer file.mkv -vf cropdetect
```

Egy 384x288-as videón kipróbálva ehhez hasonló eredményt ír ki a program:

```
[CROP] Crop area: X: 0..383  Y: 37..250  (-vf crop=384:208:0:40)
```

A program külön ellenőrzi a képkockákat, de ha szerencsénk van, akkor azonos vastagságúak a csíkok.

Tesztelhetjük, hogy a javasolt crop paraméterezés megfelelő-e, mielőtt 
[mencoder](http://www.mplayerhq.hu/DOCS/HTML/hu/mencoder.html)-rel átkonvertáljuk a fájlt:

```
mplayer file.mkv -vf crop=384:208:0:40
```