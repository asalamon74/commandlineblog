---
layout: post
title: 'pdf készítése képekből - A4'
permalink: https://commandline.blog.hu/2015/12/14/pdf_keszitese_kepekbol_a4
post_id: 8169236
categories: 
- pdf
- jpeg
- imagemagick
- A4
---

Jópár évvel ezelőtt 
[írtam](http://commandline.blog.hu/2010/03/23/pdf_keszitese_kepekbol), hogy képekből így lehet pdf-et készíteni:

```
convert *.jpg kepek.pdf
```

A módszer egyik hátránya, hogy nem mondjuk meg, mekkora oldalak vannak a pdf-ben, ami néhány pdf megjelenítő vagy nyomtató programban gondot okozhat.

Ha egyértelművé akarjuk tenni, hogy A4-es oldalat szeretnék 150dpi-vel akkor kicsit bővebb parancsra van szükségünk:

```
 convert *.jpg -resize 1241x1756 -units PixelsPerInch -density 150x150 -repage 1241x1756 kepek.pdf
```

A webes példákban többnyire 1240x1754-es, 1240x1753-as felbontás szerepel, de amikor utánaszámoltam, nekem 1241x1756 jött ki.

 