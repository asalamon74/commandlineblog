---
layout: post
title: 'exiftool if'
permalink: /2017/04/04/exiftool_if
post_id: 12397147
categories: 
- if
- exiftool
---

Az 
[exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)oldalán olvastam ezt a figyelmeztetést:

>If you find the need to use "find" or "awk" in conjunction with ExifTool, then you probably haven't discovered the full power of ExifTool. Read about the 
```
-ext
```
, 
```
-if
```
, 
```
-p
```
 and 
```
-tagsFromFile
```
 options in the 
[application documentation](http://www.sno.phy.queensu.ca/%7Ephil/exiftool/exiftool_pod.html).


Nos, valóban szoktam használni find-ot (sőt, cut-ot, grep-et...) exiftoollal, szóval megnéztem az ajánlott opciók közül if-et.

Tegyük fel van rengeteg képünk amiket különféle fényképezőgépekkel készítettünk. Azon belül pedig természetesen különféle beállításokkal. A következő paranccsal megkereshetjük a Pentax K-x géppel ISO 400-as beállítással készült képeket és kilistázhatjuk a rekeszt és az expozíciós időt:

```
$ exiftool -aperture -shutterSpeed -if '$Model eq "PENTAX K-x"' -if '$ISO eq 400' ~/Pictures/2016*
======== /home/user/Pictures/20160304/imgp7890.jpg
Aperture                        : 13.0
Shutter Speed                   : 1/60
======== /home/user/Pictures/20160305/imgp7891.jpg
Aperture                        : 13.0
Shutter Speed                   : 1/60
   58 directories scanned
  587 files failed condition
    2 image files read
```