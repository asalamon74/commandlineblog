---
layout: post
title: 'Expozíciósorozat-egyesítés'
permalink: /2013/12/23/expoziciosorozat-egyesites
post_id: 5696286
categories: 
- exiftool
- enfuse
- align_image_stack
---

Ha olyan témát szeretnénk lefényképezni ahol túl nagy az eltérés a legvilágosabb és a legsötétebb részek között, akkor a fényképezőgép korlátozott dinamikatartománya miatt az eredmény elég kiábrándító lesz. Ha a sötét részekre mérünk fényt akkor a világos részeknél csak egynemű fehér foltot kapunk, ha a világos részekre akkor a sötét részek lesznek teljesen feketék. Ha nagyon nagy a kontraszt akkor egyszerre lesz a kép sötét része teljesen fekete és a világos része teljesen fehér.

Ha expozíciósorozatot készítünk ( 
[bracketing](http://en.wikipedia.org/wiki/Bracketing) ) ahol az egyes képeknél eltér a záridő ( de minden egyéb paraméter megegyezik ), akkor már sokkal több esélyünk van arra, hogy minden részlet rendesen látszódjon, persze eltérő képeken:

![ef_input_0470.jpg](/assets/ef_input_0470.jpg)

Már csak össze kell illeszteni a különböző képeket. Az egyik lehetőség a HDR ( valójában inkább 
[HDR + tonemapping](http://photo.stackexchange.com/q/7630/507) ), de számomra szimpatikusabb az expozíciósorozat-egyesítés ( exposure fusion ). A különbséget itt nem részletezném, akit érdekel 
[itt](http://photo.stackexchange.com/a/20897/507) talál egy részletes leírást.

Egy kis scriptet készítettem, ami 3 DNG fájlt egyesít:

```
#!/bin/bash
x1=`printf '%04d' $1`;
x2=`printf '%04d' $(( $1+1 ))`;
x3=`printf '%04d' $(( $1+2 ))`;
efname=imgp${x1}_ef
ufraw-batch --temperature=5500 --out-type=png imgp${x1}.dng imgp${x2}.dng imgp${x3}.dng
align_image_stack -s 3 -a ais_imgp${x1}_ imgp${x1}.png imgp${x2}.png imgp${x3}.png
enfuse -o ${efname}.tif ais_imgp${x1}_*.tif
convert ${efname}.{tif,jpg}
exiftool -TagsFromFile imgp${x1}.png -all:all ${efname}.jpg
exiftool '-DateTimeOriginal>FileModifyDate' ${efname}.jpg
exiftool -P -keywords+="exposure fusion"  ${efname}.jpg
rm ais_imgp${x1}_*.tif
rm ${efname}.tif
rm ${efname}.jpg_original
rm imgp${x1}.png imgp${x2}.png imgp${x3}.png
```

A script először 
[konvertálja](/2010/05/11/raw_konvertalasa_jpg_re) a DNG fájlokat png-re majd egymáshoz illeszti a képeket ( erre a lépésre nincs szükség ha stabil állványt használtunk ). A tényleges egyesítést 
[enfuse](http://enblend.sourceforge.net/) végzi, majd átmásolom az exif adatokat, 
[beállítom a fájl módosítási dátumát](/2012/06/05/cim-nelkul_6547) és az "exposure fusion" 
[kulcsszót](/2012/06/08/digitalis_fenykepek_felcimkezese). A legvégén törlöm a felesleges fájlokat.

A script használata egyszerű, ha imgp0470.dng, imgp0471.dng, imgp0472.dng fájlokat akarom egyesíteni:

```
exposure_fusion.sh 470
```

![imgp0470_ef.jpg](/assets/imgp0470_ef.jpg)
