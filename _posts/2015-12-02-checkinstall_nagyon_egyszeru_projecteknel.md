---
layout: post
title: 'checkinstall nagyon egyszerű projecteknél'
permalink: /2015/12/02/checkinstall_nagyon_egyszeru_projecteknel
post_id: 8121872
categories: 
- checkinstall
- install
- rpm
---

[Írtam](/2010/01/25/checkinstall) már a checkinstallról, amivel rpm (deb, ...) csomagot készíthetünk egy olyan projectből ami make install segítségével települne fel, kikerülve a csomagkezelőt.

Vannak olyan egyszerű projectek, ahol még make install sincsen, jellemzően egyetlen futtatható fájl keletkezik, és azt kézzel kell átmásolni a /usr/local/bin (vagy ~/bin) alkönyvtárba.

Ezeknél a projecteknél is használható checkinstall. Példaként installáljuk a qimport fájlt a /usr/local/bin alkönyvtárba:

```
checkinstall install -m 0755 qimport /usr/local/bin
```

A parancs legyártja a /home/user/rpmbuild/RPMS/x86_64/qimport-20151128-1.x86_64.rpm csomagot, amit utána már könnyen installálhatunk.

Többnyire -s (strip) kapcsolót is szoktam használni install parancsnál, de valamiért checkinstall ezt nem szereti.