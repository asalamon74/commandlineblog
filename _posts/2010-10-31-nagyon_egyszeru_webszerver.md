---
layout: post
title: 'Nagyon egyszerű webszerver'
permalink: https://commandline.blog.hu/2010/10/31/nagyon_egyszeru_webszerver
post_id: 2411173
categories: 
- python
- http
- webszerver
---

A következő paranccsal az aktuális alkönyvtár tartalmát érhetjük el egy nagyon egyszerű webszerveren keresztül: 
```
python -m SimpleHTTPServer
``` 
Ideális, ha html oldalakat editálunk, de nem szeretnénk az igazi webszerverünkön keresztül elérhetővé tenni az éppen editált oldalakat, vagy nem szeretnénk a webszerver konfigurációval foglalkozni. 
A webszervert a 8000-es porton keresztül érhetjük el: 
```
http://$HOSTNAME:8000/
``` 
```
$HOSTNAME
```
 helyett a gépünk nevét kell írni, mondjuk én az egyszerűség kedvéért 
```
127.0.0.1
```
-et szoktam.