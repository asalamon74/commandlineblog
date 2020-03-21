---
layout: post
title: 'script + scriptreplay'
permalink: /2013/10/05/script_scriptreplay
post_id: 5551628
categories:  []
---

Időnként hasznos elmenteni, hogy mit is dolgozunk egy terminálban, de egy 
[videó mentése](http://commandline.blog.hu/2013/05/26/recordmydesktop) azért túlzásnak tűnik.

Egyszerűbb az util-linux csomagban található 
[script](http://en.wikipedia.org/wiki/Script_%28Unix%29) programot használni:

```
script -t 2> timing.txt -a session.txt
```

A parancs hatására látszólag semmi sem történik, dolgozhatunk tovább, egészen addig amíg az exit parancsot be nem gépeljük ( vagy CTRL-D-t nem nyomunk ), ekkor 2 fájl keletkezik. session.txt tartalmazza magát a mentést, timing.txt pedig az időzítést, vagyis innen lehet tudni mit milyen gyorsan gépeltünk, az egyes programok mit mikor írtak ki a terminálba.

Ha vissza szeretnénk játszani a felvett anyagot, akkor a következőképpen tehetjük meg:

```
scriptreplay timing.txt session.txt
```

Nem igazán értem, hogy miért, de az én disztribúciómban util-linux csomag csak a script parancsot tartalmazza, scriptreplay-t nem. Van ennek egy perl verziója, 
[innen](http://www.ifokr.org/bri/presentations/tools/scriptreplay) töltöttem le.