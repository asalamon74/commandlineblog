---
layout: post
title: 'mkv vágása'
permalink: https://commandline.blog.hu/2016/09/30/mkv_vagasa
post_id: 11753643
categories: 
- mkv
- ffmpeg
---

Egy hosszabb mkv fájlból újrakódolás nélkül kivághatunk részleteket ffmpeggel:

```
ffmpeg -i hosszu.mkv -t 21.5 -c copy rovid.mkv
```

A fenti parancs az első 21.5 másodpercből készít új fájlt. Ha nem a fájl legeleje kell nekünk, akkor -ss kapcsolót kell használnunk.