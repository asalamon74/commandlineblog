---
layout: post
title: 'bash ctrl-r'
permalink: /2010/01/28/bash_ctrl_r
post_id: 1634681
categories: 
- bash
---

Azt szinte mindenki tudja, hogy a bash megjegyzi a korábbi parancsokat ( alapesetben a 
```
~/.bash_history
```
 fájlban ), és a korábbi parancsokat a felfele nyíllal érhetjük el. Ez kényelmes, ha egy nem túl régi parancsot keresünk, de elég kényelmetlen, ha egy olyan parancsot, amelyet néhány napja (hete) futtattunk. ( Gyakran látom, hogy többen ilyenkor 20-30 alkalommal lenyomják a felfele nyilat, hátha megtalálják a parancsot. Többnyire nem, vagy csak nagyon lassan sikerül. ).Ennél sokkal egyszerűbb a 
```
ctrl-r
```
 használata. A billentyűkombinációt lenyomva 
```
(reverse-i-search)
```
 módba kerülünk, és a korábbi parancs egy tetszőleges részét beírva könnyen megtalálhatunk egy régi parancsot.