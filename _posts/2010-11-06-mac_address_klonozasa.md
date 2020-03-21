---
layout: post
title: 'MAC address klónozása'
permalink: /2010/11/06/mac_address_klonozasa
post_id: 2425749
categories: 
- mac_address
- ifconfig
---

Minden hálózati eszköznek saját (elvileg egyedi) 
[címe](http://hu.wikipedia.org/wiki/MAC-c%C3%ADm) van. Bár elvileg nagyon jó dolog az egyedi cím, számtalan esetben jól jöhet, ha ezt a címet átírhatjuk. Például az internetszolgáltatók gyakran a MAC addresshez kötik a szolgáltatást, és ha gépet ( alaplapot, hálózati kártyát ) cserélünk, akkor sokkal egyszerűbb az új gépünkön beállítani a régi gép címét mint a szolgáltatót megkérni, hogy írja át a címet az adatbázisában. 
A címet a következőképpen tudjuk átírni ideiglenesen: 
```
ifconfig eth0 down
 ifconfig eth0 hw ether 01:23:45:67:89:ab up
``` 
```
eth0
```
 helyett értelemszerűen a módosítandó interfész nevét kell megadnunk, 
```
01:23:45:67:89:ab
```
 helyett pedig a kívánt MAC addresst.Bár nem feltétlen kell, én többnyire a művelet előtt leállítom az egész hálózatot ( 
```
/etc/init.d/network stop
```
 ) utána pedig újraindítom ( 
```
/etc/init.d/network start
```
 ). 
A fenti címmódosítás csak ideiglenes, a következő újraindítás során visszaáll a régi cím. Ha állandó módosítást szeretnénk, akkor         
```
/etc/sysconfig/network-scripts/ifcfg-eth0
```
 fájlba ( feltéve, ha 
```
eth0
```
 címét akarjuk módosítani ) kell a következő sor: 
```
MACADDR=01:23:45:67:89:ab
```