---
layout: post
title: 'Szimbolikus link módosítása'
permalink: /2011/07/27/szimbolikus_link_modositasa
post_id: 3099922
categories: 
- szimbolikus_lunk
---

A 
[szimbolikus linkek](http://en.wikipedia.org/wiki/Symbolic_link) használata igen sokszor megkönnyíti az életünket. Tipikus példája a használatuknak amikor egy folyamatosan változó verziójú fájlnál egy link mutat a legutolsó verzióra: 
```
 ls -l /lib/libz*
 lrwxrwxrwx 1 root root    13 2010-10-29 15:56 /lib/libz.so.1 -> libz.so.1.2.3
 -rwxr-xr-x 1 root root 74760 2010-01-06 15:05 /lib/libz.so.1.2.3
``` 
A programoknak elég annyit tudni, hogy a 
```
libz.so.1
```
 fájlra van szükségük. Ha kijön az 1.2.4 verzió, akkor egyszerűen le lehet cserélni a linket, nem kell a programokat módosítani. 
Eddig ha le kellett cserélnem egy szimbolikus linket, akkor 2 lépésben tettem meg. Tegyük fel 
```
alma.txt
```
 nevű linkünk 
```
alma-2.3.4.txt
```
-re mutat, de 
```
alma-2.3.5.txt
```
-re szeretnénk cserélni: 
```
rm alma.txt
 ln -s alma-2.3.5.txt alma.txt
``` 
A két parancsot persze 
[&&](http://commandline.blog.hu/2010/02/06/bash_parancsok_egymas_utan) segítségével kötöttem össze. 
Nemrég botlottam bele egy sokkal egyszerűbb megoldásba: 
```
ln -sf alma-2.3.5.txt alma.txt
``` 
Ha pedig még 
[kevesebbet](http://commandline.blog.hu/2010/04/20/bash_zarojeles_kiegeszites) szeretnénk gépelni: 
```
ln -sf alma{-2.3.5,}.txt
``` 
  
Azt azért érdemes megjegyezni, hogy valójában ez sem atomi művelet, vagyis ha egy nagyon fontos fájlra mutató linket cserélünk így le, akkor van egy rövid időszak ameddig a link sehová sem mutat. 
  
 