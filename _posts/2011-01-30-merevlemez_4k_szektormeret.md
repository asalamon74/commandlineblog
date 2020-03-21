---
layout: post
title: 'Merevlemez 4K szektorméret'
permalink: /2011/01/30/merevlemez_4k_szektormeret
post_id: 2578199
categories: 
- merevlemez
- hdd
- fdisk
---

Mivel a merevelemezek mérete folyamatosan nő ( miközben kb. 20 ezer forintért vettem az összes merevlemezem ) időnként a bizonyos szabványok túlhaladottá válnak. A legutóbbi fontos változás a szektor méret megnövelése volt. A korábbi 512 byte helyett ma már jellemzően 4096 byte a szektor mérete (bővebben 
[itt](http://superuser.com/q/132729/8240) olvashatunk erről). 
Az operációs rendszereket folyamatosan felkészítették ennek támogatására, vagyis (hacsak nem valami régi rendszert használunk) elvileg nem is kellene ezzel foglalkoznunk. A gyakorlatban azonban több olyan merevlemez van, amelyik (talán kompatibilitási okokból) továbbra is 512 byte-os szektorméretet jelent az operációs rendszer felé ( 
```
fdisk -l
```
 részlet): 
```
Sector size (logical/physical): 512 bytes / 512 bytes
``` 
Elvileg egy jumper segítségével lehet ezt állítani, de erről egyrészt sok helyen lebeszélik az embert, másrészt pedig egyszerűbbnek tűnt szoftveresen megoldani a problémát. 
A gond az 512 byte-os szektormérettel az, hogyha az alapértelmezett beállításokkal (255 fej, 63 szektor/track) partícionáljuk a merevlemezt, akkor rögtön az első partíció a 63. szektoron kezdődik. Mivel ez nem egyezik a fizikai szektor kezdetével (mert 63 nem osztható nyolccal) ezért a merevlemez írási/olvasási sebessége alacsonyabb lesz. 
Mivel nem igazán lenne kényelmes egyenként ellenőrizni a partíciók kezdetének pozícióját, 
```
fdisk
```
et érdemes inkább rávenni arra, hogy ezt elvégezze helyettünk. Erre a legegyszerűbb módszer az, ha 
```
fdisk
```
nek azt adjuk meg, hogy a default értékek helyett inkább 224 fejjel és 56 szektor/track értékekkel dolgozzon: 
```
fdisk -H 224 -S 56 /dev/sdb
``` 
Ezek után ha létrehozzuk a partíciós táblát és a partíciókat, akkor az első partíció már az 56. szektoron kezdődik: 
```
# fdisk -lu /dev/sdb
 
 Disk /dev/sdb: 1500.3 GB, 1500301910016 bytes
 224 heads, 56 sectors/track, 233599 cylinders, total 2930277168 sectors
 Units = sectors of 1 * 512 = 512 bytes
 Sector size (logical/physical): 512 bytes / 512 bytes
 I/O size (minimum/optimal): 512 bytes / 512 bytes
 Disk identifier: 0x22dd6918
 
    Device Boot      Start         End      Blocks   Id  System
 /dev/sdb1              56  2930265855  1465132900   83  Linux
``` 
 
A parancssorban persze mindenki cserélje le /dev/sdb-t a megfelelő címre!