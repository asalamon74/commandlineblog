---
layout: post
title: 'virtualbox hdd méretnövelés'
permalink: /2016/04/15/virtualbox_hdd_meretnoveles
post_id: 8606516
categories: 
- hdd
- gparted
- virtualbox
- ntfsresize
- VBoxManage
---

A szokásokkal ellentétben most nem egy parancsot mutatok be, hanem egy valódi probléma megoldását. Hasonlóan a korábbi 
[HDD - SSD](/2011/11/25/hdd_le-rol_ssd-re) cseréhez.

Linux alatt virtualboxban (5.0.14) fut egy windowsos gépem, ahol 10GB-os mérete van a C: drive-nek. Nem tudom miért csak ekkora méretet választottam, valószínűleg azt gondoltam elég lesz. De nyilván nem lett elég. Később egy új HDD-t is adtam a virtuális gépnek és átpakoltam pár dolgot, de újabban megint kicsinek tűnik a C: drive, windows egyfolytában panaszkodik, takarítás sem segített. Vagyis a feladat a virtuális gépen a C: drive méretének megnövelése, nyilván újrainstall nélkül. Leginkább 
[ezt](http://www.libtronics.com/2011/07/resize-virtualbox-disk-for-winxp-guest.html)a leírást próbáltam követni, de sokmindent másként kellett csinálnom.

Az egyszerűség kedvéért az összes alkönyvtár helyett minden példában /path-ot írok.

Virtualboxnak van 
[parancssoros eszköze](https://www.virtualbox.org/manual/ch08.html) szerencsére.

Először is kilistázom a virtuális gépeket, csak hogy biztos legyek benne, hogy parancssorból is látom a gépem, majd információt kérek a gépről.

```
VBoxManage list vms
 VBoxManage showvminfo nyul_xp
```

A parancs nagyon sok adatot megad, számomra csak ennyi fontos most:

```
...
 IDE Controller (0, 0): /path/nyul_xp.vdi (UUID: 57657647-a880-4e0b-9fc3-4651dc7cffa8)
IDE Controller (0, 1): /path/nyul_xp_second.vdi (UUID: 2b916d2f-4730-4ad3-b4c8-29bfb27d49e8)
IDE Controller (1, 0): /path/VBoxGuestAdditions_4.1.18.iso (UUID:45308f05-f80e-4bc4-8b39-ec3e700ac5b1)
 ...
```

Vagyis 3 meghajtó van a gépen. nyul_xp.vdi (C:) és nyul_xp_second.vdi (E:) merevlemezek és VBoxGuestAdditions_4.1.18.iso (D:) optikai meghajtó. 
Hogy miért van 4.1.18-as VBoxGuestAdditions az 5-ös virtualboxomban azt nem tudom, de most nem is fontos.

Letöltöttem 
[gparted live](/2011/11/10/gparted_live)-ot, és ezt teszem a virtuális gép virtuális DVD-meghajtójába:

```
VBoxManage storageattach "nyul_xp" --storagectl "IDE Controller" --port 1 --device 0 --type dvddrive --medium /path/gparted-live-0.25.0-3-i686.iso
```

Ezután ellenőriztem, tényleg gparted live bootol-e be (igen).

```
VBoxManage startvm "nyul_xp"
```

Visszatérve linux parancssorba (az eredeti Linux gép parancssorába, nem a virtuális gép gparted parancssorába) kilistáztam a virtuális gépek HDD-jeit:

```
VBoxManage list hdds
```

A listában ott volt a fent is látott nyul_xp.vdi, így megnöveltem ennek a méretét:

```
VBoxManage modifyhd 57657647-a880-4e0b-9fc3-4651dc7cffa8 --resize 20000
VBoxManage clonehd 57657647-a880-4e0b-9fc3-4651dc7cffa8 nyul_xp_20.vdi
```

Valamiért feltétlenül UUID-vel kellett hivatkoznom a merevlemezre. A fenti két parancs eredménye egy új nyul_xp_20.vdi, a clonehd parancs kiírta az új UUID-t is, de arra végül nem volt szükség.

Ezután az új megnövelt méretű merevlemezre cseréltem a régit a virtuális gépben:

```
VBoxManage storageattach "nyul_xp" --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium /path/nyul_xp_20.vdi
```

Ezután a virtuális gépet be lehet bootolni, gparted live indult el. A grafikus felület nem működött, de amúgy is parancssorban akartam dolgozni.

Először is 
[parted](http://www.gnu.org/software/parted/manual/parted.html) segítségével megnöveltem a partíció méretét (resizepart alparancs). Ezt nyilván nem így kellett volna, fdisk-et is használhattam volna, de balga módon azt hittem, hogy parted automatikusan átméretezi a fájlrendszert is. Nem tette, vagyis nem kerülhettem el ntfsresize használatát:

```
ntfsresize --info /dev/sda1
 ntfsresize -n -s 20971M /dev/sda1
 ntfsresize -s 20971M /dev/sda1
```

A --info kapcsolóval tudtam meg, mekkora méretre kell növelnem a fájlrendszert. Először -n kapcsolóval futtattam, ami csak szimulálja a módosításokat, majd utána élesben.

Itt újraindítottam a virtuális gépből, és azt választottam induláskor, hogy ne gparted hanem a windows induljon el. Windows persze először panaszkodott és ellenőrizte az új meghajtót, de második bootra már rendben elindult. De azért javasolt még egy bootot is.

Mivel gparted live-ra nincsen szükség, utolsó lépésként a virtuális gépben visszacseréltem a DVD-t:

```
VBoxManage storageattach "nyul_xp" --storagectl "IDE Controller" --port 1 --device 0 --type dvddrive --medium /path/VBoxGuestAdditions_4.1.18.iso
```

 