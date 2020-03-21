---
layout: post
title: 'bash parancsok egymás után'
permalink: https://commandline.blog.hu/2010/02/06/bash_parancsok_egymas_utan
post_id: 1686870
categories: 
- bash
- "&&"
---

Az egyik első dolog amit bash parancsokkal kapcsolatban a dokumentációk megemlítenek, az hogy nagyon egyszerű szekvenciálisan egymás után végrehajtani a parancsokat, elég pontosvesszővel elválasztani őket: 
```
parancs1; parancs2; parancs3
``` 
A fenti módszerrel a három parancsot egymás után végrehajtjuk, függetlenül azok eredményétől. Az esetek többségében ez nem veszélyes, de egyszer egy ismerősöm a következő parancsot adta ki a 
```
/
```
 alkönyvtárban: 
```
cd /itt/egy/nagyon/bonyolt/es/hosszu/alkonyvtar/volt; rm -rf *
``` 
és sajnos közben elírta a nagyon hosszú alkönyvtár címét... 
Hacsak lehetséges kerüljük a 
```
;
```
 használatát parancsok elválasztásakor, és használjuk helyette az 
```
&&
```
 operátort, ami csak akkor hatja végre a második parancsot, ha az első sikeresen lefutott (vagyis nullát adott visszatérő értéknek). A fenti igen kellemetlen meglepetéseket így elkerülhetjük. 
```
parancs1 && parancs2 && parancs3
``` 
  
 