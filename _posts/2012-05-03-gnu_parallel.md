---
layout: post
title: 'GNU parallel'
permalink: https://commandline.blog.hu/2012/05/03/gnu_parallel
post_id: 4481862
categories: 
- find
- parallel
- xargs
- basename
---

Bár 
[find](http://commandline.blog.hu/2010/11/14/find_2) + 
[xargs](http://commandline.blog.hu/2011/01/06/xargs) segítségével rengeteg érdekes problémát meg tudunk oldani, túlzás lenne azt állítani, hogy a túl kényelmes a két parancs használata. A neve alapján GNU 
[parallel](http://www.gnu.org/software/parallel/)ről azt gondoltam, hogy csak a párhuzamos feldolgozásban ( lásd 
[xargs -P](http://commandline.blog.hu/2011/01/12/xargs_p) ) fog segíteni, de némi használat után úgy látom hogy a párhuzamosságon kívül a használata is egyszerűbb.

Ha egy alkönyvtár png fájljait szeretném jpeg formátumra átkonvertálni és egyben átméretezni, akkor a find + xargs használatával a következőképpen tehetem ezt meg:

```
find . -name '*.png' | xargs -n1 -i basename {} .png | xargs -P 2 -n1 -i convert -resize 1200x1200 {}.png {}_web.jpg
```

Ha xargs helyett parallelt használok, akkor több kapcsolóra és a basename használatára sincsen szükség:

```
find . -name '*.png' | parallel convert -resize 1200x1200 {} {.}_web.jpg
```

Következő lépésben a find-ot is megszüntethetjük a ::: használatával:

```
parallel convert -resize 1200x1200 {} {.}_web.jpg ::: *.png
```

Ha egyszerre szeretnék két méretre is átméretezni, akkor erre is van lehetőségünk:

```
parallel convert -resize {2}x{2} {1} {1.}_{2}.jpg ::: *.png ::: 1200 300
```

 A parancs hatására alma.png fájlból alma_300.jpg, alma_1200.jpg fájlokat kapjuk.

Számtalan példát írhatnék még, de szerintem egyszerűbb a program írójának, Ole Tangénak a bemutatását megnézni: