---
layout: post
title: 'GPS adatok másolása'
permalink: /2011/02/05/gps_adatok_masolasa
post_id: 2551678
categories: 
- gps
- exiftool
- digitális_fénykép
---

Bár nyilván az a legkényelmesebb, ha fényképezőgépünk magától elvégzi a fényképek 
[geotaggelését](http://hu.wikipedia.org/wiki/Geotagging), a gyakorlatban mégis gyakran manuálisan kell a GPS koordinátákat beállítanunk. Ha több fényképet is azonos helyen készítettünk, akkor elég egyetlen képnél beállítani az adatokat, majd a következő paranccsal másolhatjuk át a koordinátákat a többi fényképbe: 
```
exiftool -P -overwrite_original_in_place -tagsfromfile input.jpg -gps:all output.jpg
``` 
A 
```
-P
```
 kapcsoló hatására a fájl dátuma változatlan marad.