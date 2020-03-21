---
layout: post
title: 'Fájlok átnevezése kisbetűssé'
permalink: https://commandline.blog.hu/2010/05/20/fajlok_atnevezese_kisbetusse
post_id: 2003832
categories: 
- for
- seq
- tr
---

A sztringmanipulással, pontosabban karakterek cseréjével (illetve törlésével) foglalkozó 
[tr](http://linux.about.com/library/cmd/blcmdl1_tr.htm) parancs működését többnyire egy igen egyszerű példán mutatják be. Ha pl. egy sztringben az összes a, b, c betűket rendre d, e, f betűkre szeretnénk cserélni, akkor 
```
tr abc def
``` 
parancsot kell használnunk, és ezután a begépelt szavakban megtörténik a csere. 
Ennél azért lényegesen hasznosabb a következő script, amivel egy alkönyvtár összes .JPG fájlját nevezhezjük át kisbetűssé (nemcsak a kiterjesztést, hanem a teljes fájlnevet): 
```
for i in *.JPG; do mv $i `echo $i | tr A-Z a-z`; done
``` 
A rövid script megértésében segít a 
[for ciklusról](http://commandline.blog.hu/2010/05/17/bash_for_ciklus) illetve 
[seq](http://commandline.blog.hu/2010/04/08/seq)-ról szóló bejegyzés.