---
layout: post
title: 'Digitális fénykép dátumának módosítása'
permalink: /2011/05/23/digitalis_fenykep_datumanak_modositasa
post_id: 2918974
categories: 
- pentax
- exiftool
- digitális_fénykép
---

Ha a digitális fényképezőgépen véletlenül pontatlanul állítjuk be a dátumot akkor 
[exiftool](http://commandline.blog.hu/2010/05/14/exiftool) segítségével javíthatjuk ki a hibát. Tételezzük fel (csak a teszt kedvéért persze), hogy 1 nappal elállítottam véletlenül a dátumot: 
```
$ exiftool -a imgp1955.dng | grep 2011
 File Modification Date/Time     : 2011:05:21 08:03:30+02:00
 Modify Date                     : 2011:05:21 08:03:27
 Date/Time Original              : 2011:05:21 08:03:27
 Create Date                     : 2011:05:21 08:03:27
 Date                            : 2011:05:21
``` 
Bár a dátumok arra utalnak, hogy 21-én készült a felvétel, valójában 20-án. A következő paranccsal javíthatjuk meg a hibás dátumokat: 
```
$ exiftool -AllDates-=24 -Pentax:Date-=1 *.dng 
     4 image files updated
```
 Ezután már helyes dátumokat látszódnak: 
```
$ exiftool -a imgp1955.dng | grep 2011
 File Modification Date/Time     : 2011:05:20 11:54:24+02:00
 Modify Date                     : 2011:05:20 08:03:27
 Date/Time Original              : 2011:05:20 08:03:27
 Create Date                     : 2011:05:20 08:03:27
 Date                            : 2011:05:20
``` 
Pár dolog azért látszik a dátumjavító parancsnál:* Egyszerre több képet is kezel a parancs (fenti példában négyet).
* Elegendő megadni mennyivel szeretnénk eltolni a dátumokat, nem kell egyenként megadni a helyes dátumokat. Ha heteken keresztül készítettük a fényképeket elállított dátummal, akkor ez nagyon hasznos.
* Neve ellenére az 
```
AllDates
```
 nem az összes dátumot módosítja, nem kezeli a gyártóspecifikus dátum mezőket. Ezért kellett külön megadnom a 
```
Pentax:Date
```
 mezőt.
* ```
AllDates
```
 és 
```
Pentax:Date
```
 nem egyforma formátumban várja a számokat, ezért adom meg az 1 napot eltérő módon. 
 