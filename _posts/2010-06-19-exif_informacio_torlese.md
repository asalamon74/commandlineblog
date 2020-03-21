---
layout: post
title: 'exif információ törlése'
permalink: /2010/06/19/exif_informacio_torlese
post_id: 2093130
categories: 
- exif
- imagemagick
- digitális_fénykép
- mogrify
---

Bár a digitális fényképekben tárolt 
[EXIF](http://hu.wikipedia.org/wiki/Exif) információ igen hasznos lehet, nem biztos hogy szerencsés ha bárki 
[ki tudja olvasni](http://commandline.blog.hu/2010/05/14/exiftool) a publikus képeink adatait. Publikálás előtt törölhetjük az információkat a 
[mogrify](http://www.imagemagick.org/www/mogrify.html)parancs ( a már többször említett 
[ImageMagick](http://www.imagemagick.org/) csomag része ) segítségével: 
```
mogrify -strip *.jpg
```