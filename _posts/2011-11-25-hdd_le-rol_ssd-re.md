---
layout: post
title: 'HDD lecserélése SSD-re'
permalink: /2011/11/25/hdd_le-rol_ssd-re
post_id: 3394267
categories: 
- windows
- linux
- hdd
- ssd
- dd
- xxd
- fdisk
---

A korábbi bejegyzésekkel ellentétben itt nem egy parancsot mutatok be, hanem egy valódi probléma megoldását. Egy elég öreg Windows XP-s laptopban cseréltem ki a HDD-t (merevlemezt) 
[SSD](http://hu.wikipedia.org/wiki/SSD)-re. A feladat során a következő céljaim voltak:

* Windows XP újrainstall nélkül megoldani az egészet,


* miközben a HDD-nél kisebb SSD-t szerelek be,


* az egyészet linuxos parancssorral oldom meg (különben hogyan írnék róla ide?),


* az egész folyamat során nem írok a HDD-re (vagyis baj esetén sem történhet nagy baj).  

## Eszközök


Egy 
[pendrive-ról](http://commandline.blog.hu/2011/11/10/gparted_live) bootoltam Linuxot, így nem volt szükség külön linuxos gépre. A következő eszközökre fogok hivatkozni a leírásban:

* /dev/sda:  Az eredeti 80GB-os HDD.


* /dev/sdb: A pendrive (ezt nem fogom használni).


* /dev/sdc: Egy kellően nagy háttértár.


* /dev/sdd: Az új 64GB-os SSD.

Ha valaki a leírást szeretné követni, akkor persze ellenőrizze, hogy nála milyen névvel kell hivatkozni az eszközökre. 

## HDD tartalmának lementése


Első lépésként a régi merevlemez teljes tartalmát 
[elmentettem](http://commandline.blog.hu/2011/11/13/dd_merevlemez_backup) egy nagy fájlba:

```
mkdir /mnt/diskc
mount /dev/sdc1 /mnt/diskc
dd if=/dev/sda of=/mnt/diskc/sda.img
```

## NTFS partíció átméretezése


Az így elmentett sda.img fájl partícióit ellenőriztem fdisk segítségével:

```
$ fdisk -l /mnt/diskc/sda.img
Disk /mnt/diskc/sda.img: 80.0 GB, 80026361856 bytes
240 heads, 63 sectors/track, 10337 cylinders, total 156301488 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x94e494c4
             Device Boot      Start         End      Blocks   Id  System
/mnt/diskc/sda.img1   *          63   138907439    69453688+   7  HPFS/NTFS/exFAT
/mnt/diskc/sda.img2       138907440   156295439     8694000    c  W95 FAT32 (LBA)
```

A 2. partíció a Windows XP install anyagát tartalmazza, ezt nem fogom átmásolni az SSD-re, a továbbiakban csak az 1. partícióval foglalkozok. Az első partíciót 
[losetup](http://commandline.blog.hu/2011/11/22/losetup) segítségével érhetjük el:

```
losetup -o $((63*512)) /dev/loop1 /mnt/diskc/sda.img
mkdir /mnt/diska1
mount /dev/loop1 /mnt/diska1
umount /mnt/diska1
```

A partíció átméretezéséhez az 
[ntfsresize](http://www.tuxera.com/?id=ntfsresize) programot használtam:

```
$ ntfsresize --info /dev/loop1
ntfsresize v2011.4.12AR.7 (libntfs-3g)
Device name        : /dev/loop1
NTFS volume version: 3.1
Cluster size       : 4096 bytes
Current volume size: 71120577024 bytes (71121 MB)
Current device size: 80026329600 bytes (80027 MB)
Checking filesystem consistency ...
 Accounting clusters ...
Space in use       : 59315 MB (83.4%)
Collecting resizing constraints ...
You might resize at 59314573312 bytes or 59315 MB (freeing 11806 MB).
Please make a test run using both the -n and -s options before real resizing!
$ ntfsresize -n -s 63500 /dev/loop1
$ ntfsresize -s 63500 /dev/loop1
```

Az első parancs alapvető információkat ír ki a partícióról, a legfontosabb az, hogy mi az a legkisebb méret amire át lehet méretezni (59315 MB). A második paranccsal szimulálom a 63.5GB-re méretezést. Ennek eredményeként azt írta a program, hogy minden menni fog. Az utolsó parancs végzi a tényleges munkát.

Érdemes megjegyezni, hogy egyáltalán nem biztos, hogy minden átméretezés sikerül ami --info alapján lehetségesnek tűnik. Teszt során nekem úgy tűnt, érdemes minél több helyet felszabadítani. Mások töredezettségmentesítésre esküsznek. Kétszer egymás után.

## MBR átmásolása


 A HDD-ről át kell másolni az 
[MBR](http://en.wikipedia.org/wiki/Master_boot_record)-t az új SSD-re. Bár elvileg az első szektor tartalmazza az MBR-t, és a leírás alapján elegendő lenne az első 440 (vagy 446) byte átmásolása (hiszen utána a partíciós tábla található), egy NTFS boot rekordot bemutató 
[leírás](http://thestarman.pcministry.com/asm/mbr/NTFSBR.htm) (amiből többet meg lehet tudni az NTFS bootról mint amennyit valaha szerettem volna megtudni) alapján az ezt követő szektorok is tartalmaznak hasznos információt. Az egyszerűség kedvéért átmásoltam mindent ami az első partíció előtt található a merevlemezen:

```
dd if=/mnt/diskc/sda.img of=/dev/sdd bs=512 count=62
```

Utólag írva a leírást már látom, hogy a fenti logika alapján valójában 63 szektort kellett volna átmásolni 62 helyett, de a gyakorlatban ez nem fontos.

## Partíciós tábla módosítása


Az előző másolás során az eredeti partíciós tábla adatai is átmásolódtak, ami nyilván teljesen rossz. Először is fdisk segítségével töröltem a 2 eredeti partíciót, majd fdisk-et újraindítottam. Ezután létrehoztam egy új partíciót ami elfoglalja a teljes 64GB-ot. Típusa ugyanolyan ( 7 - HPFS/NTFS/exFAT ) mint az eredeti 1. partíció. Ezt a partíciót bootolhatóvá tettem. Az új partíciós tábla:

```
Disk /dev/sdd: 64.0 GB, 64023257088 bytes
22 heads, 16 sectors/track, 355242 cylinders, total 125045424 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x94e494c4
   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048   125045423    62521688    7  HPFS/NTFS/exFAT
```

Látszik az is, hogy itt már nem a 63. szektoron kezdődik a partíció, hanem a 2048. szektoron. 
[Itt](http://prohardver.hu/teszt/mindent_az_ssd-krol/particio_kezdetenek_eltolasa.html) olvashatunk bővebben arról, hogy ez miért is jó. 

## Partíció tartalmának átmásolása


A már korábban említett 
[losetup](http://commandline.blog.hu/2011/11/22/losetup) segítségével létrehoztam egy eszközt ami a SSD 1. partíciójára mutat, és átmásoltam az átméretezett partíció tartalmát (63.5GB-ot).

```
losetup -o $((2048*512)) /dev/loop2 /dev/sdd
dd if=/dev/loop1 of=/dev/loop2 bs=512 count=$((63500000000/512))
```

## NTFS boot rekord módosítása


Ahogy a már említett 
[NTFS Boot leírás](http://thestarman.pcministry.com/asm/mbr/NTFSBR.htm) említi, illetve ahogy némileg érthetőbben 
[itt](http://www.2pi.info/software/copying-windows-new-hard-drive.html) is le van írva, mivel az SSD-n az 1. partíció nem ugyanazon a pozíción kezdődik mint ahogy a HDD-n kezdődőtt, ezért módosítanunk kell a partíció első szektorában a "Hidden Sector Count" értékét. A következő 
[dump](http://commandline.blog.hu/2010/03/20/dump) mutatja az 1. partíció tartalmának első 32 byte-ját:

```
0000000 eb 52 90 4e 54 46 53 20 20 20 20 00 02 08 00 00
0000020 00 00 00 00 00 f8 00 00 
3f 00 f0 00 3f 00 00 00
```

A kijelölt rész a következő 3 számot tartalmazza (
[little endian](http://hu.wikipedia.org/wiki/Byte-sorrend) byte-sorrendben):  63, 240, 63. Az első két számot nem módosítottam, de a 3. számot 2048-ra írtam át 
[xxd](http://commandline.blog.hu/2011/11/19/xxd_382) segítségével:

```
echo 00: 3F 00 F0 00 00 08 | xxd -r > /mnt/diskc/ntfs_change.dat
dd if=/mnt/diskc/ntfs_change.dat of=/dev/sdd1 bs=1 count=6 seek=24
```

Felmerülhet e kérdés, minek írok 6 byte-ot, ha csak 2-t változtatok meg. Nos, a fenti dokumentációk alapján úgy tűnt, hogy a szektor/track és fejek száma mezőket is módosítani kell az fdisk által jelzett új értékekre. Így nem volt hajlandó bootolni az SSD, így végülis visszaírtam az eredeti értékeket.

Nem igazán világos, hogy mi értelme van egy partíció első szektorára felírni azt, hogy hol is kezdődik a partíció. Ezt az adatot csak akkor tudjuk beolvasni, ha már amúgy is tudjuk a partíció helyét.

## Végső lépések


Ennél a pontnál kikapcsoltam a gépet és átszereltem a régi HDD helyére az SSD-t, majd bebootoltam Windows XP-t. Elsőre persze panaszkodott, hogy valami babrálta a merevlemezt ( ntfsresize állítja be a flaget ) ezért ellenőrzést futtatott. Ezután bootolt, majd jelezte hogy új hardvert talált. Ezután megint bootolt, és minden működött rendben.