---
layout: post
title: 'tar autocompress'
permalink: /2010/04/11/tar_autocompress
post_id: 1894687
categories: 
- tar
---

A 
[tar](http://www.gnu.org/software/tar/) program elég régóta támogatja többféle külső tömörítőprogram használatát: 
kapcsoló             
tömörítőprogram 
-Z, --compress             
[compress](http://www.opengroup.org/onlinepubs/9699919799/utilities/compress.html)         
--lzma             
[lzma](http://tukaani.org/lzma/)         
-z             
[gzip](http://www.gzip.org/)         
-J, --xz             
[xz](http://tukaani.org/xz/)         
--lzop             
[lzop](http://www.lzop.org/)         
 -j, --bzip2             
[bzip2](http://www.bzip.org/) 
  
Lehetőségünk van a felsoroltakon kívül 
[más tömörítőprogram használatára](http://commandline.blog.hu/2010/01/13/tar_pbzip2) is. 
Egyrészt persze hasznos hogy sok tömörítőprogram közül választhatunk, másrészt könnyen összekeverhetjük a kapcsolókat. Sokkal egyszerűbb, ha az automatikus tömörítőprogram választást használjuk. 
Kitömörítésnél egyszerűen lehagyhatjuk a tömörítőprogram kiválasztását befolyásoló kapcsolót, és tar a kiterjesztés alapján választ. Vagyis 
```
tar xvfz teszt.tgz
``` 
helyett használhatjuk a következő egyszerűbb verziót: 
```
tar xvf teszt.tgz
``` 
Tömörítésnél a 
```
--auto-compress
```
 ( rövid verzió: 
```
-a
```
 ) kapcsolóval aktiválhatjuk a kiterjesztés alapú tömörítőprogram választást. 
```
tar cvfz teszt.tgz *.txt
 tar cvfj teszt.tbz *.txt
``` 
helyett: 
```
tar cvfa teszt.tgz *.txt
 tar cvfa teszt.tbz *.txt
``` 
 