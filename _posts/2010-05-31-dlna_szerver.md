---
layout: post
title: 'dlna szerver'
permalink: https://commandline.blog.hu/2010/05/31/dlna_szerver
post_id: 2041691
categories: 
- szerver
- dlna
- minidlna
---

Ahogy egyre több "kütyü" tud lejátszani médiafájlokat, egyre nagyobb az igény, hogy ezeket a fájlokat ne egyenként másoljuk át a megfelelő eszközökre, hanem egy központi helyen tároljuk, amit minden eszköz elérhet. A valószínűleg egyre jobban elterjedő 
[DLNA](http://www.geeks.hu/technologiak/090406_dlna_minden_kapcsolodik) szabványt persze legjobban akkor használhatjuk ki, ha dedikált médiaszerverünk van, a gyakorlatban azonban egy linuxos gép is könnyen lehet DLNA-szerver. 
A sok elérhető szoftver közül az egyik legegyszerűbbről a 
[minidlna](http://minidlna.sourceforge.net/)-ról írok itt. 
A szerver konfigurálásához a 
```
minidlna.conf
```
fájlt kell módosítani, nagy eséllyel elegendő megadni azt, hogy a fájlrendszer melyik részét szeretnénk megosztani: 
```
media_dir=/ezt/osztjuk/meg
``` 
A szerver elindítása: 
```
minidlna -R -f /konfigfajlhelye/minidlna.conf
``` 
Érdemes még megjegyezni, hogy minidlna (még) nem végez semmilyen konverziót, vagyis médialejátszóink csak akkor tudják lejátszania  fájlokat, ha felismerik a formátumot.