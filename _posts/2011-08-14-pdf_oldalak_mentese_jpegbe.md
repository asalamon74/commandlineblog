---
layout: post
title: 'pdf oldalak mentése jpegbe'
permalink: https://commandline.blog.hu/2011/08/14/pdf_oldalak_mentese_jpegbe
post_id: 3150635
categories: 
- pdf
- convert
- jpg
- imagemagick
---

Arról már 
[írtam](http://commandline.blog.hu/2010/03/23/pdf_keszitese_kepekbol), miként tudunk sok jpg fájlból egy pdf fájlt készíteni, most az ellentétes irányt mutatom meg, amikor egy pdf oldalait mentjük el jpeg fájlokba: 
```
convert input.pdf output_%02d.jpg
``` 
Az eredményt oldalanként 1 jpeg fájl: 
```
output_00.jpg, output_01.jpg, output_02.jpg...
``` 
Alapesetben 72dpi-nek megfelelő fájlok készülnek, de ezt módosíthatjuk, ha jobb minőségre van szükségünk: 
```
convert -density 300 input.pdf output_%02d.jpg
``` 
A fenti esetben az összes oldalt konvertálja a parancs, ha erre nincsen szükségünk, megadhatjuk a konvertálandó oldalak sorszámát. Ha az 5. 6. 7. oldalt szeretnénk csak feldolgozni: 
```
convert -density 300 input.pdf[5-7] output_%02d.jpg
``` 
Érdemes még megjegyezni, hogy egy bug miatt[imagemagick](http://www.imagemagick.org/)6.6-ban néha csak az első oldalt konvertálta a parancs, az újabb verzióban már javították a bugot.