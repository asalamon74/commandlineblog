---
layout: post
title: 'recordmydesktop'
permalink: /2013/05/26/recordmydesktop
post_id: 5306388
categories:  []
---

A kettővel ezelőtti 
[bejegyzéshez](/2013/05/20/pv_cdialog) csatolt videó miatt szükségem volt a képernyőm egy részének rögzítésére. Ehhez 
[recordmydesktopot](http://recordmydesktop.sourceforge.net) használtam:

```
$ recordmydesktop -windowid $(xwininfo |grep "Window id:"|sed -e "s/xwininfo\:\ Window id:\ // ;s/\ .*//" ) --no-sound --no-cursor --fps 2 -o felvetel.ogv
```

Némi magyarázat:

* -windowid paraméterrel kell megadni, hogy melyik ablakot szeretnénk rögzíteni. Egy ablak azonosítószámát az 
[xwininfo](http://www.xfree86.org/4.2.0/xwininfo.1.html) paranccsal lehet megtudni, ami egy egérkattintásra vár.


* --no-sound: hang nem kell


* --no-cursor: az egérkurzort sem szeretném rögzíteni


* --fps 2: másodpercenkénti 2 kép elég


* -o felvetel.ogv: az output fájl neve.