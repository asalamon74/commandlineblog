---
layout: post
title: 'fuse-lgefs'
permalink: https://commandline.blog.hu/2014/05/30/fuse-lgefs
post_id: 6234361
categories: 
- lg
- fuse
- fuse-lgefs
---

Néhány évvel ezelőtt elég népszerűek voltak a merevlemezes DVD-felvevők. A kissé félrevezető név azt jelenti, hogy analóg TV-adásokat lehetett rögzíteni merevlemezre, majd később a felvételeket át lehetett venni DVD-re is. Komoly előrelépés volt egy ilyen a videómagnó után, de a digitális átállás után ezek is eléggé elavultak.

Nekem egy LG RH7500-as készülékem van amiben a DVD író/olvasó már nem működik rendesen, így a merevlemezen lévő felvételekhez nem férek hozzá (valamiért az összes ilyen eszköz közös jellemzője, hogy macerás a felvételekhez férni, még véletlenül sincs pl. hálózati csatlakozójuk).

Szétszedtem a készüléket, kiszereltem a merevlemezt. Mivel teljesen szabványos IDE HDD ezért csatlakoztatni tudtam a számítógéphez. Rögtön jelezte a gép, hogy nincs rajta partíciós tábla, de az adatokat lementettem egy fájlba:

```
$ dd if=/dev/sdc of=lg_7500.dat bs=1M
```

Beleolvasva a fájlba, úgy tűnik, hogy FAT32 partíció van rajta:

```
$ string lg_7500.dat | head -n 10
LGEINC  
VOLUMELABE FAT32   
LGEINC  
VOLUMELABE FAT32   
RRaA
rrAa
RRaA
rrAa
RRaA
rrAau`
```

Alaposabban megvizsgálva viszont látszik, hogy nem szabványos FAT32-ről van szó, hanem valami módosított verzióról, vagyis nem lehet egyszerűen felmountolni. Némi keresés után rátaláltam a 
[fuse-lgefs](http://code.google.com/p/fuse-lgefs/) projectre, amivel hozzá lehet férni az adatokhoz. Bár azt írja a feljesztő, hogy csak LG RHT-388H-ból kiszerelt merevlemezzel tesztelte, nagyszerűen működött LG RH7500-nál is:

```
$ lgefuse lg_7500.dat /mnt/test
 $ ls -ltr /mnt/test
total 0
drwxr-xr-x 2 root root          0 Jan  1  2000 B/
drwxr-xr-x 2 root root     524288 Jan  1  2004 MEDIA/
-r--r--r-- 1 root root 1057282048 Feb 23  2007 00001407007d7223072720.str
-r--r--r-- 1 root root     119692 Feb 23  2007 00001407007d7223072720.idx
-r--r--r-- 1 root root 2353827840 Sep  7  2008 00020a04017d8730005001.str
-r--r--r-- 1 root root     751248 Sep  7  2008 00020a04017d8730005001.idx
-r--r--r-- 1 root root 2145730560 Aug 23  2009 00000a02007d9823205459.str
-r--r--r-- 1 root root     810684 Aug 23  2009 00000a02007d9823205459.idx
-r--r--r-- 1 root root 2623533056 Jan 15  2010 00000c01007da115212459.str
-r--r--r-- 1 root root     986884 Jan 15  2010 00000c01007da115212459.idx
-r--r--r-- 1 root root 1505107968 Jun 15  2010 00030a07027da613075121.str
-r--r--r-- 1 root root     142848 Jun 15  2010 00030a07027da613075121.idx
-r--r--r-- 1 root root 1162661888 Jan 12  2012 00000a1a007dc112100235.str
-r--r--r-- 1 root root     130292 Jan 12  2012 00000a1a007dc112100235.idx
-r--r--r-- 1 root root 9151928320 Sep 20  2013 00000a03007dd920151459.str
-r--r--r-- 1 root root    1022124 Sep 20  2013 00000a03007dd920151459.idx
-r--r--r-- 1 root root 8582496256 Nov  8  2013 00000a03007ddb08151459.str
-r--r--r-- 1 root root     958748 Nov  8  2013 00000a03007ddb08151459.idx
-r--r--r-- 1 root root 7336847360 Mar 28 17:20 00000a03007de328152430.str
-r--r--r-- 1 root root     820156 Mar 28 17:20 00000a03007de328152430.idx
-r--r--r-- 1 root root 9152591872 May  9 18:40 00000a03007de509151459.str
-r--r--r-- 1 root root    1022180 May  9 18:40 00000a03007de509151459.idx
-r--r--r-- 1 root root 1251153920 May 15 23:26 00000a06007de515211759.str
-r--r--r-- 1 root root     479428 May 15 23:26 00000a06007de515211759.idx
-r--r--r-- 1 root root 2450837504 May 18 23:09 00000b06007de518195759.str
-r--r--r-- 1 root root     923452 May 18 23:09 00000b06007de518195759.idx
-r--r--r-- 1 root root 1860700160 May 20 01:30 00000c04007de519224959.str
-r--r--r-- 1 root root     705020 May 20 01:30 00000c04007de519224959.idx
-r--r--r-- 1 root root 1784250368 May 21 00:26 00000d05007de520214959.str
-r--r--r-- 1 root root     676828 May 21 00:26 00000d05007de520214959.idx
```

A ritka ronda fájlnevek elsőre zavarónak tűnhetnek, a .str fájlok tartalmazzák a felvételeket, amiket pl. mplayer gond nélkül lejátszik.