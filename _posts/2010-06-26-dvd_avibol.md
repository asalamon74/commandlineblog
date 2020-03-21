---
layout: post
title: 'DVD aviból'
permalink: https://commandline.blog.hu/2010/06/26/dvd_avibol
post_id: 2108609
categories: 
- dvd
- avi
- mencoder
---

Ha egy avi fájlból szeretnénk DVD-videót készíteni, első lépésként megfelelő mpeg formátumra kell konvertálnunk. A következő példában mencoder segítségével konvertáljuk át a fájlt: 
```
mencoder input.avi -vf scale=720:576,harddup -ovc lavc -oac lavc -lavcopts acodec=mp2:abitrate=128:vcodec=mpeg2video:vstrict=0:aspect=4/3:keyint=25:vrc_buf_size=1835:vbitrate=5500:vrc_maxrate=5500:vrc_minrate=5500 -o output.mpg -of mpeg -mpegopts format=dvd:tsaf
``` 
Ha már kész az mpeg, akkor legegyszerűbben 
[dvdauthor](http://commandline.blog.hu/2010/03/05/dvdauthor) segítségével írhatunk belőle DVD-t.