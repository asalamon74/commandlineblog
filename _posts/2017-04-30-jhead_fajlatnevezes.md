---
layout: post
title: 'jhead fájlátnevezés'
permalink: https://commandline.blog.hu/2017/04/30/jhead_fajlatnevezes
post_id: 12456167
categories: 
- digitális_fénykép
- jhead
---

Fényképek tömeges átnevezésekor talán a legegyszerűbb eszköz a 
[jhead](http://www.sentex.net/~mwandel/jhead/). A következő parancs a kép készítésének időpontja alapján nevezi át a jpeg fájlokat:

```
jhead -n%Y%m%d_%H%M%S_%f *.jpg
```

A futtatás után imgp1000.jpg fájlból 20170428_100145_imgp1000.jpg lesz. Többféle formátumot használhatunk, nekem a fenti példa főleg akkor hasznos, ha több géppel fényképezek egyszerre, ezzel időrendbe lehet tenni a fájlokat. (Persze többnyire csak 
[ezután](http://commandline.blog.hu/2011/05/23/digitalis_fenykep_datumanak_modositasa))

 
Biztos meg lehet ezt oldali exiftoollal is, ha igen, otegi megírja.