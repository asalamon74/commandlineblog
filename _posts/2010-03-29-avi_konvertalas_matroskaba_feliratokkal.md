---
layout: post
title: 'avi konvertálás matroskába feliratokkal'
permalink: /2010/03/29/avi_konvertalas_matroskaba_feliratokkal
post_id: 1841706
categories: 
- felirat
- avi
- matroska
- mkvmerge
- mkvtoolnix
---

Az avi konténerformátum egyik nagy hiányossága, hogy (legalábbis eredeti formájában) nem támogatja a feliratok beágyazását. A 
[matroska](http://www.matroska.org/) tervezésekor erre már figyeltek, így ha avi fájlt konvertálunk matroskába 
[MKVToolnix](http://www.bunkus.org/videotools/mkvtoolnix/) segítségével, akkor a feliratokat is kezelhetjük. 
Tegyük fel van egy 
```
film.avi
```
 fájlunk (videó + angol hang), ezen kívül  
```
film_en.srt
```
 az angol, 
```
film_hu.srt
```
 a magyar feliratokat tartalmazó fájl. Utóbbi  
```
utf-8
```
 kódolású. A következő paranccsal készíthetjük el a 
```
film.mkv
```
 fájlt: 
```
mkvmerge -o film.mkv --language 1:eng film.avi --language 0:eng film_en.srt --language 0:hun film_hu.srt
``` 
A 
```
--language
```
 kapcsoló segítségével először a hangsáv, majd a feliratok nyelvét határozzuk meg.