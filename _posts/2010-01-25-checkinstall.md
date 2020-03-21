---
layout: post
title: 'checkinstall'
permalink: /2010/01/25/checkinstall
post_id: 1638759
categories: 
- checkinstall
- deb
- rpm
---

A Linux disztribúciók többsége rendelkezik valamilyen ( többnyire rpm vagy deb alapú ) csomagkezelő rendszerrel, amivel kényelmesen installálhatunk programokat. Bár a repository-k rengeteg programot tartalmaznak, időnként manuálisan ( forráskódot letöltve, majd a programot lefordítva ) kell programokat installálnunk. Az így telepített programok persze jól működnek, de zavaró lehet, hogy nem látszanak a csomagkezelőben. Ezen a problémán segít a 
[checkinstall](http://www.asic-linux.com.mx/~izto/checkinstall/) program, ami képes a manuális programinstallálást nyomon követni, és rpm ( vagy deb, vagy tgz ) csomagot készíteni.

Alapesetben a 
```
make install
```
 parancsot hajtja végre checkinstall, de ha kell megadhatjuk, hogy mit futtasson ( pl. 
```
checkinstall ./install.sh
```
 ).

A program elég ügyesen felismeri mit szeretnénk installálni, de persze lehetőségünk van a csomag paramétereinek módosítására:

```
1 -  Summary: [ Dvdwizard ]

2 -  Name:    [ dvdwizard ]

3 -  Version: [ 0.6.1 ]

4 -  Release: [ 1 ]

5 -  License: [ GPL ]

6 -  Group:   [ checkinstall ]

7 -  Architecture: [ i586 ]

8 -  Source location: [ dvdwizard-0.6.1 ]

9 -  Alternate source location: [  ]

10 - Requires: [  ]

11 - Provides: [ dvdwizard ]
```

Ha minden jól sikerült, akkor checkinstall elkészíti az rpm-et, de nem installálja, így ellenőrízhetjük minden rendben ment-e. Ha optimisták vagyunk, akkor persze kérhetünk automatikus installálást is. A fenti példában szereplő dvdwizard installálása során készített rpm a következő fájlokat tartalmazza:

```
[root@machine etc]# rpm -ql dvdwizard 

/etc

/etc/dvdwizard.conf

/etc/dvdwizard.conf.old

/usr

/usr/local

/usr/local/bin

/usr/local/bin/chaptercheck

/usr/local/bin/dvdcpics

/usr/local/bin/dvdtguess

/usr/local/bin/dvdwizard

/usr/local/bin/mk_vmgm

/usr/local/bin/mk_vtsm

/usr/local/bin/mk_vtsm_info

/usr/local/bin/mk_vtsm_lang

/usr/local/bin/mpgprobe

/usr/local/bin/txt2png

/usr/local/share

/usr/local/share/dvdwizard

/usr/local/share/dvdwizard/dvdwizardrc

/usr/local/share/man

/usr/local/share/man/man1

/usr/local/share/man/man1/dvdwizard.1.lzma

/usr/local/share/man/man1/mk_vmgm.1.lzma

/usr/local/share/man/man1/mk_vtsm.1.lzma

/usr/local/share/man/man5

/usr/local/share/man/man5/dvdwizard.conf.5.lzma

/usr/share

/usr/share/doc

/usr/share/doc/dvdwizard

/usr/share/doc/dvdwizard/CHANGELOG

/usr/share/doc/dvdwizard/COPYING

/usr/share/doc/dvdwizard/README

/usr/share/doc/dvdwizard/TODO

/usr/share/doc/dvdwizard/doc

/usr/share/doc/dvdwizard/doc/dvdwizard.1

/usr/share/doc/dvdwizard/doc/dvdwizard.conf.5

/usr/share/doc/dvdwizard/doc/mk_vmgm.1

/usr/share/doc/dvdwizard/doc/mk_vtsm.1
```

 