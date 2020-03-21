---
layout: post
title: 'getcap + setcap'
permalink: /2014/08/23/getcap_setcap
post_id: 6621147
categories: 
- ls
- capability
- setcap
- getcap
---

A fényképezőgépvezérlő programomban ( 
[pkTriggerCord](http://pktriggercord.sourceforge.net/) ) elég alacsony szinten kommunikálok a fényképezőgéppel, 
[ioctl](http://en.wikipedia.org/wiki/Ioctl) és 
[scsi_generic](http://sg.danny.cz/sg/) segítségével lényegében direkt módon érem el a device fájlt ( pl. /dev/sdc ). Egy ideje feltűnt, hogy hiába tűnik úgy hogy van írási és olvasási jogom is /dev/sdc-hez, mégis csak akkor működik a program ha rootként futtatom.

Némi utánaolvasás után rájöttem (valahogy ez eddig nekem kimaradt), hogy egy ideje Linuxban is igen részletesen lehet szabályozni, hogy egy process milyen jogokkal bír, vagyis ha csak egyetlen speciális jogra van szükségünk, akkor nem kell root-ként ( vagy setuid rootként ) futtatni a programot, elég ezt az egyetlen jogot megadni. A jogok listáját 
[itt](http://linux.die.net/man/7/capabilities) nézhetjük meg.

Mint kiderült, nekem a CAP_SYS_RAWIO jog kell:

```
$ getcap pktriggercord-cli
$ setcap CAP_SYS_RAWIO+eip pktriggercord-cli
 $ getcap pktriggercord-cli
 pktriggercord-cli = cap_sys_rawio+eip
```

Vagyis először lekérdezve látszik, hogy a programnak nincs semmilyen különleges joga, majd miután beállítjuk a CAP_SYS_RAWIO-t a lekérdezés után már látszik a jog. Ezután már nem kell rootként futtatnom a programomat.

1. megjegyzés: A legtöbb helyen azt írják, a CAP_SYS_RAWIO olyan erős jogosultság, hogy ennyi erővel akár rootként is lehetne futtatni a programot, az sem lenne sokkal nagyobb biztonsági rés.

2. megjegyzés: Elég alattomos mellékhatás, hogy nem igazán látszik, hogy egy programnak valami különleges jogosultsága van. A setuid bitet mondjuk sokan felismerik, de az alap ls -l nem ír ki semmit amiből látszik a különleges jog. Szerencsére a 
[színes ls](http://commandline.blog.hu/2014/08/20/ls_szinek) piros színnel jelzi ezt.