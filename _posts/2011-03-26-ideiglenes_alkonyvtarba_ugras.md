---
layout: post
title: 'Ideiglenes alkönyvtárba ugrás'
permalink: /2011/03/26/ideiglenes_alkonyvtarba_ugras
post_id: 2771034
categories: 
- cd
- alkönyvtár
---

Ha csak azért szeretnénk egy alkönyvtárba belépni, mert ott végre kell hajtanunk egy parancsot, de nem szeretnénk abban az alkönyvtárban maradni, akkor elég kényelmetlen, hogy a végén egy új 
```
cd
```
 utasítással kell visszajönnünk eredeti alkönyvtárunkba. 
Egy egyszerű zárójellel megoldhatjuk a problémát: 
```
(cd /tmp && ls -l)
``` 
A fenti parancsnál csak ideiglenesen lépünk 
```
/tmp
```
 alkönyvtárba, a végén visszajutunk oda ahol kiadtuk a parancsot.Értelme persze ennek nincs sok az ls parancsnál, de bonyolultabb esetben hasznos lehet.