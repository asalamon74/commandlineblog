---
layout: post
title: 'bash változó kapcsos zárójelben'
permalink: /2010/11/23/bash_valtozo_kapcsos_zarojelben
post_id: 2459587
categories: 
- bash
- változó
- kapcsos_zárójel
---

Viszonylag egyszerű bash scriptek írásakor is szükségünk van változókra. Nemrég beleszaladtam egy ezzel kapcsolatos problémába. Nézzük a következő példákat: 
```
[gep]$ i=1; echo $i
 1
 [gep]$ i=1; echo alma_$i
 alma_1
 [gep]$ i=1; echo alma_$i.tgz
 alma_1.tgz
 [gep]$ i=1; echo alma_$i_02.tgz
 alma_.tgz
``` 
Egészen az utolsó sorig minden rendben van és logikusnak tűnik, de ott kissé meglepett, hogy nem 
```
alma_1_02.tgz
```
 íródott ki. Rövid gondolkodás után persze rájöttem, hogy mivel nem jelzi semmi a változó nevének a végét, ezért bash nem tudja kitalálni, hogy a változó neve "i" és utána jön a _02 sztring, ehelyett azt hiszi, hogy "i_02" a változó neve. 
Persze van mód arra, hogy pontosabban jelezzük mi is a változó neve, kapcsos zárójelet kell használni. Bár korábban lustaságból nem mindig használtam, ezután igyekszem: 
```
[gep]$ i=1; echo alma_${i}_02.tgz
 alma_1_02.tgz
``` 
 