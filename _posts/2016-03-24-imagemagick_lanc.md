---
layout: post
title: 'imagemagick lánc'
permalink: https://commandline.blog.hu/2016/03/24/imagemagick_lanc
post_id: 8522324
categories: 
- imagemagick
---

Elég 
[sokszor](http://commandline.blog.hu/tags/imagemagick) írtam már az imagemagickről, ami az egyik legjobb parancssoros képszerkesztő eszköz.

Ha egy bonyolult imagemagick scriptet írok, akkor gyakran valami ilyen lesz a végeredmény:

```
#!/bin/bash
WIDTH=$(identify -ping -format "%w" $1)
HEIGHT=$(identify -ping -format "%h" $1)
convert -size ${WIDTH}x${HEIGHT} radial-gradient:black-white temp1.png
convert $1 -colorspace gray temp2.png
convert $1 temp1.png -compose Multiply -composite -normalize temp3.png
convert $1 temp2.png -compose Minus -composite temp4.png
convert temp4.png -auto-level -modulate 200 +dither -colors 2 -colorspace gray -contrast-stretch 0 temp5.png
convert temp5.png -blur 20x20 temp6.png
convert temp5.png -negate temp7.png
convert temp7.png -blur 20x20 temp8.png
convert temp8.png temp3.png -compose Multiply -composite temp9.png
convert temp6.png $1 -compose Multiply -composite temp10.png
convert temp9.png temp10.png -compose Plus -composite output.png
```

Az nem túl fontos, hogy mit csinál a script, de látszik, hogy 11 lépésből áll, közben rengeteg ideiglenes fájlt gyárt ( amit 
[trap](http://commandline.blog.hu/2016/03/17/trap_948)-pel illik a végét letakarítani ).

A fenti scriptet átírthatjuk úgy, hogy egyetlen egy parancs legyen:

```
#!/bin/bash
WIDTH=$(identify -ping -format "%w" $1)
HEIGHT=$(identify -ping -format "%h" $1)
convert $1 \
    \( -size ${WIDTH}x${HEIGHT} radial-gradient:black-white \) \
    \( -clone 0 -colorspace gray \) \
    \( -clone 0 -clone 1 -compose Multiply -composite -normalize \) \
    \( -clone 0 -clone 2 -compose Minus -composite \) \
    \( -clone 4 -auto-level -modulate 200 +dither -colors 2 -colorspace gray -contrast-stretch 0 \) \
    \( -clone 5 -blur 20x20 \) \
    \( -clone 5 -negate \) \
    \( -clone 7 -blur 20x20 \) \
    \( -clone 8 -clone 3 -compose Multiply -composite \) \
    \( -clone 6 -clone 0 -compose Multiply -composite \) \
    \( -clone 9 -clone 10 -compose Plus -composite \) \
    -delete 0-10 \
output.png
```

A következő módon működik a script:

* **convert**
: Egyetlen egyszer kell convert-et hívni.


* **$1**
: Először is felsorolom az input képeket, ezeket convert megszámozza 0-tól kezdve. Fenti példában egyetlen input kép ($1) van, ez lesz a 0. kép.


* **\( ... \)**
: Ez egyes alparancsok \( és \) között szerepelnek. Illik új sorba törni őket, hogy legyen egy kis esélyünk megérteni a scriptet.


* Látszik, hogy nem határozunk meg output fájlt az alparancsoknál. Imagemagick szépen tovább számozza az elkészült fájlokat. A radial-gradient lesz az 1. a gray a 2. ...


* Ha hivatkoznunk kell a korábbi fájlokra, akkor 
**-clone index**
 segítségével tehetjük ezt meg.


* **-delete 0-10**
: A legvégén eldobhatjuk az ideiglenes fájlokat. A fenti script 12 fájlt ( 0. 1. .... 11. ) gyárt, ebből csak az utolsó kell nekünk, égy a 0. indextől a 10. indexig törölhetjük a felesleges fájlokat.


* **output.png**
: A végső eredményt ide írjuk ki.


* Ha töröljük a -delete részt, akkor output-0.png, output-1.png ... néven elmenti a script a részeredményeket is, ez elég hasznos, ha debuggolunk.

A script gyorsabb mint az eredeti verzió, mert nem kell png-re konvertálással, fájlba mentéssel, fájlból olvasással, png dekódolással tölteni az időt.

Látszik, hogy az indexekre eléggé oda kell figyelni, ha a script elejét módosítjuk, akkor a későbbi indexeket módosítani kell. Ezen lehet kicsit segíteni, ha kicsit átírjuk a scriptet:

```
convert $1 \
    \( -size ${WIDTH}x${HEIGHT} radial-gradient:black-white \) \
    \( -clone 0 -colorspace gray \) \
    \( -clone 0 -clone 1 -compose Multiply -composite -normalize \) \
    \( -clone 0 -clone 2 -compose Minus -composite \) \
    \( +clone -auto-level -modulate 200 +dither -colors 2 -colorspace gray -contrast-stretch 0 \) \
    \( +clone -blur 20x20 \) \
    \( -clone 5 -negate \) \
    \( +clone -blur 20x20 \) \
    \( +clone -clone 3 -compose Multiply -composite \) \
    \( -clone 6 -clone 0 -compose Multiply -composite \) \
    \( -clone 9 +clone -compose Plus -composite \) \
    -delete 0--2 \
output.png
```

* Az előző lépésben létrejött képre hivatkozhatunk 
**+clone**
 paranccsal.


* Használhatnám +clone helyett az azzal ekvivalens
**-clone -1**
-et is.


* Ha a kettővel korábbi képre akarunk hivatkozni, akkor 
**-clone -2**
 kellene.


* **delete 0--2**
: A -2. index az utolsó előtti képet jelenti.0--2 valójában a 0. indextől a -2. indexig tartó intervallumot jelenti, vagyis ezzel lehet az utolsó kép kivételével az összeset törölni.

 