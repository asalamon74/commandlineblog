---
layout: post
title: 'imagemagick'
permalink: https://commandline.blog.hu/2010/01/22/imagemagick
post_id: 1636589
categories: 
- convert
- imagemagick
- képméretezés
---

Ha képekkel dolgozunk, akkor nyilván rengeteg olyan feladat van amit grafikus felülettel rendelkező programmal ( pl. 
[gimp](http://www.gimp.org/) ) oldhatunk meg legegyszerűbben. Vannak azonban olyan esetek, amikor egyszerűbb a parancssor használata.

Az 
[ImageMagick](http://www.imagemagick.org/) az egyik legelterjedtebb parancssorból használható képmanipuláló programcsomag, melynek összetettségéről sokat elárul, hogy több ( angol nyelvű ) könyvet vásárolhatunk, ha meg szeretnénk ismerni.

A következő ( 
[convert](http://www.imagemagick.org/script/convert.php) programot használó ) egyszerű példa azt mutatja, miként tudunk egy png fájlt átméretezni (1000x1300) és jpeg formátumra ( minőség: 90% ) átkonvertálni (úgy hogy mindeközben az eredeti png is megmaradjon):

```
convert -resize 1000x1300 -quality 90% oldal_01.png oldal_01.jpg
```

A parancssor előnye persze akkor jelentkezik, ha nem egyetlen képet szeretnénk kezelni, hanem egyszerre többet. A következő paranccsal az összes 
```
oldal_*.png
```
 fájlon elvégezhetjük ugyanezt a műveletet:

```
for img in oldal_*.png; do convert -resize 1000x1300 -quality 90% $img `basename $img .png`.jpg; done
```