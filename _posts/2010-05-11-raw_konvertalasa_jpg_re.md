---
layout: post
title: 'raw konvertálása jpg-re'
permalink: /2010/05/11/raw_konvertalasa_jpg_re
post_id: 1991073
categories: 
- jpeg
- pentax
- dng
- k_x
- ufraw
- ufraw_batch
- digitális_fénykép
---

Ha digitális fényképezőgépünkkel raw formátumban (dng, pef, nef, ...) mentünk, előbb-utóbb felmerül az igény, hogy ismertebb (jpeg, tiff, ...) formátumra konvertáljuk a képeket. Linux alatt az egyik legelterjedtebb konvertáló programnak, az 
[ufraw](http://ufraw.sourceforge.net/)nak létezik parancssoros verziója is, ami igen hasznos ha egyszerre többszáz képet kell konvertálnunk. 
A következő példa Pentax K-x géppel készített dng fájlokat konvertál: 
```
ufraw-batch --rotate=no --wb=camera --crop-left=18 --crop-right=4290 --crop-top=10 --crop-bottom=2858 --out-type=jpg --compression=95 *.dng
``` 
* ```
--rotate=no
```
: Kikapcsolom az elforgatást, mert ufraw előbb forgat és utána vág, így a crop parancs hibás lenne. Gondot nem okoz, hiszen az elkészült fájl is tartalmazza az EXIF infót, így majd a képfeldolgozó program végzi az elforgatást, amikor megnyitom a jpeget.
     
* ```
--wb=camera
```
: Fehéregyensúly beállítása a fényképezőgép által dng-be mentett információk alapján.
     
* ```
--crop-left=18 --crop-right=4290 --crop-top=10 --crop-bottom=2858
```
: A kép széleinek levágása. A látszólag értelmetlen lépés okairól részletesen 
[itt](http://forums.dpreview.com/forums/read.asp?forum=1036&message=34135950) olvashatunk, lényeg, hogy levágjuk a kép jobb oldalán a fekete részt, és a végeredmény egy 4272x2848 felbontású kép lesz (az arány pont 3:2).
     
* ```
--out-type=jpg --compression=95
```
: 95%-os jpeget gyártunk
     
* ```
*.dng
```
: az alkönyvtárban lévő összes dng fájlt feldolgozzuk. 