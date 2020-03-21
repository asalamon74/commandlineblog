---
layout: post
title: 'kdenlive melt'
permalink: https://commandline.blog.hu/2012/07/06/kdenlive_melt
post_id: 4632473
categories: 
- melt
- kdenlive
- mlt
---

Ezen a blogon értthető okokból nem fogom a 
[kdenlive](http://www.kdenlive.org/)-ot bemutatni, mivel az egy grafikus felülettel használható videóeditáló program. Ugyanakkor kdenlive az 
[MLT](http://www.mltframework.org/bin/view/MLT) ( Media Lovin' Toolkit ) keretrendszerre épül, és szerencsére a projecteket leíró .kdenlive fájlformátum olyan módon bővíti az MLT által is használt 
[MLT XML](http://www.mltframework.org/bin/view/MLT/MltXml) fájlformátumot, hogy használni tudjuk az MLT parancssoros melt programját.

Én a renderelést, vagyis a végső videófájl előállítását szoktam a parancssorra bízni:

```
melt input.kdenlive -consumer avformat:output.mp4 vcodec=libx264 threads=2 b=5000k acodec=aac ab=128k tune=film preset=slow s=1280x720 aspect=@16/9 progress=1
```