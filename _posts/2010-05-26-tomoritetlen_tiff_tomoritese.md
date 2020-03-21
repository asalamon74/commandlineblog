---
layout: post
title: 'Tömörítetlen tiff tömörítése'
permalink: https://commandline.blog.hu/2010/05/26/tomoritetlen_tiff_tomoritese
post_id: 2004628
categories: 
- convert
- tiff
- imagemagick
- lzw
---

A 
[tiff](http://hu.wikipedia.org/wiki/TIFF) formátumot számos előnye miatt elég sok helyen használják. Ha pl. egy negatívtekercset digitalizáltatunk, jó eséllyel ebben a formátumban kapjuk meg a képeket. Bár számos tömörítési eljárást támogat, az egyszerűség (nagyobb kompatibilitás) kedvéért igen gyakran tömörítetlen tiff fájlokat használnak. 
Ha egy tömörítetlen tiff fájl méretét csökkenteni szeretnénk minőségromlás nélkül, akkor a támogatott tömörítési eljárások közül veszteségmentesen érdemes választani. A következő parancsor segítségével 
[LZW(Lempel-Ziv-Welch)](http://hu.wikipedia.org/wiki/LZW) tömörítést használunk: 
```
convert -compress lzw eredeti.tif tomoritett.tif
```