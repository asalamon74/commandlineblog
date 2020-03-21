---
layout: post
title: 'Digitális fényképek felcímkézése'
permalink: /2012/06/08/digitalis_fenykepek_felcimkezese
post_id: 4571901
categories: 
- exif
- seq
- exiftool
- digitális_fénykép
---

Ha egy nyaralás során több helyen is fényképezünk, akkor jellemzően fájlnév alapján egyszerűen meghatározhatunk egy intervallumot, amin belül ugyanazt a kulcsszót szeretnénk a képekhez adni. Az egyszerűség kedvéért tegyük fel, hogy 1000 képet készítettünk: imgp0000.jpg, ..., imgp0999.jpg, ezek közül imgp0053.jpg, ..., imgp0125.jpg képek a kies Helyszín település látványosságait örökítik meg. Ekkor a következő paranccsal adhatjuk hozzá a képekhez a megfelelő címkét 
[seq -f](/2012/04/06/seq_30) segítségével.

```
exiftool -P -keywords+="Helyszín" $(seq -f 'imgp%04g.jpg' 53 125)
```