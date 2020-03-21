---
layout: post
title: 'exiftool gps'
permalink: /2017/06/10/exiftool_gps
post_id: 12582951
categories: 
- gps
- exiftool
---

Fényképek GPS koordinátáját legegyszerűbben 
[exiftoollal](http://commandline.blog.hu/2010/05/14/exiftool) állíthatjuk be:

```
exiftool -GPSLongitudeRef=E -GPSLongitude=16.8436 -GPSLatitudeRef=N -GPSLatitude=46.8451 *.jpg
```

forrás: 
[https://scribblesandsnaps.com/2011/11/23/easy-geotagging-with-exiftool/](https://scribblesandsnaps.com/2011/11/23/easy-geotagging-with-exiftool/)