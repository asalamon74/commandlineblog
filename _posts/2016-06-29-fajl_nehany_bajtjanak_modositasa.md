---
layout: post
title: 'Fájl néhány bájtjának módosítása'
permalink: https://commandline.blog.hu/2016/06/29/fajl_nehany_bajtjanak_modositasa
post_id: 8853748
categories: 
- dd
- xxd
---

Korábban már 
[módosítottam](http://commandline.blog.hu/2011/11/25/hdd_le-rol_ssd-re)egy partíciós tábla fejlécében néhány bájtot 
[xxd](http://commandline.blog.hu/2011/11/19/xxd_382)és dd használatával, amikor egy fájllal akartam ugyanezt megtenni, akkor viszont nem teljesen működött a módszer:

```
dd if=/dev/zero of=test.dat bs=1 count=100
 echo 00: FF | xxd -r > ff.dat
 dd if=ff.dat of=test.dat bs=1 count=1 seek=50
```

Egy 100 bájtos tesztfájlban akartam az 51. byte-ot FF-re cserélni. Az eredmény kissé meglepő módon egy 51 bájt hosszú fájl lett, dd automatikusan levágta a fájl végét.

Ha azt szeretnénk, hogy dd ne vágja le a fájl végét és tényleg csak az 51. bájtot módosítsa, akkor a következő parancs kell (a lényeg a conv=notrunc):

```
dd conv=notrunc if=ff.dat of=test.dat bs=1 count=1 seek=50
```