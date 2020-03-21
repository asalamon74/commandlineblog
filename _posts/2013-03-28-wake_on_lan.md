---
layout: post
title: 'wake on lan'
permalink: /2013/03/28/wake_on_lan
post_id: 5176418
categories: 
- wol
- wake_on_lan
- mac_address
---

Manapság a legtöbb számítógép képes arra, hogy "kikapcsolt" állapotban is figyelje a hálózatot, és megfelelő jel esetén felébredjen. Igen hasznos ez a képesség, ha egy távoli számítógépet időnként el szeretnénk érni, de mégsem szeretnénk folyamatosan bekapcsolva hagyni.

A felébresztésnek több módja van, a 
[wol](http://sourceforge.net/projects/wake-on-lan/) programmal parancssorból is felébreszthetünk egy távoli számítógépet:

```
wol AA:BB:CC:DD:EE:FF
```

Paraméternek a gép 
[MAC-címét](http://hu.wikipedia.org/wiki/MAC-c%C3%ADm) kell megadnunk.

Arra azért figyeljünk oda, hogy a parancs nem várja meg, hogy a távoli gép feléledjen, vagyis legalább egy sleep-et tegyünk a scriptünkbe a parancs után.