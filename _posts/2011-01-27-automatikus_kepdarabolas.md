---
layout: post
title: 'Automatikus képdarabolás'
permalink: /2011/01/27/automatikus_kepdarabolas
post_id: 2551958
categories: 
- imagemagick
- fred_weinhaus
---

[ImagaMagick](http://www.imagemagick.org/) kincsesbányába botlottam. 
[Fred Weinhaus weboldalán](http://www.fmwconcepts.com/imagemagick/) számtalan imagemagickre épülő scriptet találhatunk. 
Az egyik ilyen script segítségével egy régi problémámat sikerült megoldani. Ha egyszerre több képet ( könyvborítót, fényképet, ...) 
[szkennelek be](/2011/01/15/szkenneles), akkor elég macerás egyenként kijelölni a képeket, és a kissé elfordult képeket visszaforgatni ( akár digitálisan, akár megigazítás után újraszkennelve ). 
A 
[multicrop](http://www.fmwconcepts.com/imagemagick/multicrop/) script mindezt elvégzi helyettünk. A következő képet szkenneltem be, 2 könyvborítót láthatunk rajta: 
![](/assets/egyben.jpg) 
 A következő parancs segítségével egyszerűen feldarabolhatjuk a képet: 
```
multicrop egyben.tiff konyv.tiff
``` 
 Az eredmény 2 fájl, konyv-0.tiff és konyv-1.tiff: 
![](/assets/konyv1.jpg) 
 
![](/assets/konyv2.jpg) 
A script akkor működik jól, ha a háttérszín eléggé homogén, és elüt a fényképektől. Bár ebben a példában nem volt rá szükség, automatikusan elforgatja a ferdén beszkennelt képeket.