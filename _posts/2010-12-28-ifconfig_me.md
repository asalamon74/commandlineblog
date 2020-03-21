---
layout: post
title: 'ifconfig.me'
permalink: https://commandline.blog.hu/2010/12/28/ifconfig_me
post_id: 2543375
categories: 
- curl
- wget
- ifconfig
---

Rengeteg weboldal van, aminek segítségével lekérdezhetjük hálózati csatlakozásunk adatait, de a legtöbb nem sokra használható, ha parancssorból szeretnénk ezt megtenni. Az 
[ifconfig.me](http://ifconfig.me/) oldalt viszont úgy tervezték, hogy parancssorból is könnyen elérhetőek legyenek az adatok: 
IP lekérdezése: 
```
curl ifconfig.me
``` 
vagy 
```
curl ifconfig.me/ip
``` 
Hostnév lekérdezése: 
```
curl ifconfig.me/host
``` 
Ezen kívül még sokmindent lekérdezhetünk, bővebb leírás ifconfig.me főoldalának alján található. 
Ha curl helyett inkább wgetet szeretnénk használni, akkor kicsit bonyolultabb lesz a parancssor:
```

``` 
```
wget -q -O - ifconfig.me/host
```