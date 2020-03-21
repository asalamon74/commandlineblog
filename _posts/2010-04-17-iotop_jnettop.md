---
layout: post
title: 'iotop, jnettop'
permalink: /2010/04/17/iotop_jnettop
post_id: 1909024
categories: 
- top
- iotop
- jnettop
---

A 
[top](http://linux.die.net/man/1/top) parancsot valószínűleg mindenki ismeri, ellenőrízhetjük futó programjaink mennyi memóriát, processzoridőt használnak. Igen gyakran használjuk a parancsot, hogy megtudjuk melyik programunk zabálja a memóriát, vagy terheli le a processzort.Most két igen hasonló programra hívnám fel a figyelmet, melyek nagyon hasonlóak, ám más erőforrások megfigyelésére alkalmasak:Az 
[iotop](http://guichaz.free.fr/iotop/) (érdemes 
```
-o
```
 kapcsolóval indítani, hogy csak az I/O értelemben aktív programokat listázza) az input/output műveleteket , míg 
[jnettop](http://jnettop.kubs.info/wiki/) a hálózati forgalmat figyeli hasonló módon.