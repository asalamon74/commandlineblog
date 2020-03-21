---
layout: post
title: 'nice, renice'
permalink: https://commandline.blog.hu/2011/11/01/nice_renice
post_id: 3342058
categories: 
- nice
- process
- pid
- renice
---

Ha nagyon hosszú ideig futó scripteket írunk, akkor nem túlzottan jó, ha a futás ideje alatt a gépünk nagyon belassul. Legegyszerűbb (és persze nem teljesen tökéletes) megoldás, ha alacsonyabb prioritással indítjuk el a scriptet: 
```
nice -n 19 script.sh
``` 
Ha indítás után jövünk rá, hogy a prioritáson változtatni szeretnénk, akkor a renice parancs segíthet. 
```
renice -n 19 11111
``` 
ahol 11111 a process azonosítója.