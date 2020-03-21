---
layout: post
title: 'Több matroska összefűzése'
permalink: /2010/04/02/tobb_matroska_osszefuzese
post_id: 1842303
categories: 
- mkv
- mkvmerge
- mkvtoolnix
---

Több matroska fájlt (azonos felbontás, kódolás, ...) egymás után kapcsolhatunk az 
[mkvmerge](http://www.bunkus.org/videotools/mkvtoolnix/) paranccsal: 
```
mkvmerge -o teljes.mkv resz1.mkv +resz2.mkv
``` 
Ne felejtsük el a 
```
+
```
 jelet a második input fájl neve elött, ezzel jelezzük, hogy egymás után szeretnénk a 
```
resz1.mkv
```
 
```
resz2.mkv
```
 fájlokat kapcsolni!