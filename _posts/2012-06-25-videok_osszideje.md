---
layout: post
title: 'Videók összideje'
permalink: https://commandline.blog.hu/2012/06/25/videok_osszideje
post_id: 4607680
categories:  []
---

Egy olyan scriptre volt szükségem, ami megadja, hogy az alkönyvtárban található videófájloknak mennyi az összesített hossza. Szerencsére 
[találtam egy ilyen scriptet](http://www.commandlinefu.com/commands/view/3612/get-the-total-length-of-all-video-audio-in-the-current-dir-and-below-in-hms), így nem kellett nekem megírnom:

```
find -type f -name "*.mp4" -print0 | xargs -0  mplayer -vo dummy -ao dummy -identify 2>/dev/null | perl -nle '/ID_LENGTH=([0-9\.]+)/ && ($t +=$1) && printf "%02d:%02d:%02d\n",$t/3600,$t/60%60,$t%60' | tail -n 1
```

A működés rövid magyarázata:

* [find](http://commandline.blog.hu/2010/11/14/find_2) segítségével megkeressük a minket érdeklő fájlokat ( Az eredeti példában .avi szerepelt, nekem .mp4-re volt szükségem )


* mplayer segítségével sok-sok infót iratunk ki ( innen látszik, hogy a script mindennel elboldogul, amit mplayer kezelni tud )


* Az mplayer által kiírt adatok közül az ID_LENGTH érdekes számunkra, ez másodpercben írja ki a hosszt.


* perl program(ocska) összeadja a másodperceket és óra:perc:másodperc formában kiírja


* A 
[tail](http://commandline.blog.hu/2010/08/31/head_tail) miatt csak a legutolsó sor, a végösszeg íródik ki.