---
layout: post
title: 'DVD rip mkv'
permalink: /2011/02/02/dvd_rip_mkv
post_id: 2585307
categories: 
- dvd
- mkv
- matroska
- handbrake
---

A 
[HandBrake](http://handbrake.fr/) egy igen közkedvelt videó konvertáló program, viszont úgy látom főleg a GUI verziót ismerik az emberek, a p
[arancssoros verzió](http://trac.handbrake.fr/wiki/CLIGuide) valamiért nem annyira ismert. 
A következő példában egy DVD-t konvertálunk át mkv fájlba egyetlen paranccsal: 
```
HandBrakeCLI --main-feature --markers --two-pass --turbo -i /media/cdrom -e x264 -b 2000 -B 192 --audio 1,4 --subtitle 1 -o film.mkv
``` 
A kapcsolók magyarázata: 
```
--main-feature
``` 
A kapcsoló hatására automatikusan a leghosszabb title-t választja ki a program. Az esetek túlnyomó részében ez tartalmazza a filmet amit konvertálni szeretnénk. ( A rövidebbek pedig pl. filmajánlókat ) 
```
--markers
``` 
A dvd fejezeteit megjelöli az mkv fájlban is. 
```
--two-pass
``` 
Kétlépéses kódolás. 
```
--turbo
``` 
A kódolás első lépése gyors legyen ( jelentős gyorsulás minimális minőségromlás árán ). 
```
-i /media/cdrom
``` 
Az input fájl ( esetünkben a DVD). 
```
-e x264
``` 
Az x264 encoder használata. 
```
-b 2000
``` 
Videó bitráta 2000 kb/s. 
```
-B 192
``` 
Audió bitráta 192 kb/s. 
```
--audio 1,4
``` 
A DVD 1. és 4. audió csatornáját kódoljuk bele az mkv fájlba. 
```
--subtitle 1
``` 
A DVD 1. feliratát kódoljuk bele az mkv fájlba. ( Nem a képre ráírva, hanem külön trackként). 
```
-o film.mkv
``` 
Output fájlnév.Az eredmény egy olyan mkv fájl, ami 4 tracket ( 1 videó, 2 audió, 1 felirat ) tartalmaz. 
 