---
layout: post
title: 'Kétmenetes kódolás egyszerűen'
permalink: https://commandline.blog.hu/2010/05/06/ketmenetes_kodolas_egyszeruen
post_id: 1976616
categories: 
- for
- kódolás
- bash
- ciklus
- transcode
- kétmenetes
---

A legtöbb videókonvertáló program támogatja a kétmenetes kódolásást. Egy kapcsoló segítségével határozhatjuk meg, hogy az első vagy a második menetnél járunk. Számomra kissé érthetetlen módon többnyire nincs olyan kapcsoló amivel arra kérjük a programot, egymás után futtassa le a két menetet. Legegyszerűbben egy igen egyszerű bash for ciklussal futtathatjuk le a két lépést egymás után a parancssor megismétlése nélkül: 
```
for i in 1 2; do 
 transcode ... -R $i;
 done;
``` 
A módszer akkor alkalmazható, ha a két menet során a többi paraméter (amit a ... helyére írunk) azonos.