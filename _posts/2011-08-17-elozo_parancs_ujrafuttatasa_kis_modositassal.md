---
layout: post
title: 'Előző parancs újrafuttatása kis módosítással'
permalink: https://commandline.blog.hu/2011/08/17/elozo_parancs_ujrafuttatasa_kis_modositassal
post_id: 3151305
categories: 
- bash
---

Ha parancssort használunk, elég gyakran előfordul, hogy az előző parancsot szeretnénk újrafuttatni apróbb változtatásokkal. 
Ha csak egy változtatásra van szükségünk, akkor a ^ segítségével végezhetjük el a cserét: 
```
$ echo "ez egy teszt"
 ez egy teszt
 $ ^egy^ketto
 echo "ez ketto teszt"
 ez ketto teszt
``` 
A fenti módszer az "egy" első előfordulását cseréli csak át. Ha az összeset szeretnénk, akkor kicsit bonyolultabb parancsra van szükségünk: 
```
$ echo "ez egy uj teszt. egy alma"
 ez egy uj teszt. egy alma
 $ !!:gs/egy/ketto
 echo "ez ketto uj teszt. ketto alma"
 ez ketto uj teszt. ketto alma
```
 
 Mondanom sem kell, óvatosan érdemes bánni a lehetőséggel, igen könnyen adhatunk ki hibás parancsot.