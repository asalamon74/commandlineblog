---
layout: post
title: 'rpm készítése .src.rpm-ből.'
permalink: https://commandline.blog.hu/2011/07/08/rpm_keszitese_src_rpm_bol
post_id: 3044068
categories: 
- rpm
---

Ha rpm alapú Linux disztribúciót használunk, akkor kétségtelenül az a legkényelmesebb, ha a mi disztribúciónkhoz készített bináris rpm fájlokat installálunk. Ez azonban nem mindig lehetséges, hiszen a fejlesztő elég nehezen tudja az összes számbajöhető disztribúcióhoz tartozó bináris fájlt elkészíteni. Ha egy másik rpm fájllal próbálkozunk, gyakran nem járunk szerencsével, mert valami lib verziószáma nem megfelelő. Ha rendelkezésünkre áll a forrás rpm (
```
.src.rpm
```
), akkor könnyen készíthetünk belőle binárist a saját igényeinknek megfelelően. Ha tényleg csak újrafordítani akarjuk, akkor a következő paranccsal tehetjük ezt meg a legegyszerűbben: 
```
rpmbuild --rebuild pktriggercord-0.76.00-1.src.rpm
``` 
A parancs kibontja az .src.rpm fájl, installálja a benne található forrást és .spec fájlt. Elvégzi a fordítást, majd ha minden rendben ment, eltakarít maga után, törli az installált forrást, .spec fájlt, és a fordítás során keletkezett ideiglenes fájlokat is. Az eredményül kapott rpm-et a  
```
~/rpmbuild/RPMS/
```
 egyik alkönyvtárában (pl. i386) találhatjuk, és ha szükséges, installálhatjuk.