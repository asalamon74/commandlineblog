---
layout: post
title: 'Videostabilizálás'
permalink: https://commandline.blog.hu/2017/01/01/videostabilizalas
post_id: 12085397
categories: 
- ffmpeg
- vid.stab
---

Ha nem állvánnyal készítjük a videóinkat akkor jó eséllyel remegős lesz a felvétel amit utána korrigálni illik.

A 
[vid.stab](https://github.com/georgmartius/vid.stab) könyvtár több editáló programban is megtalálható, én ffmpeggel használtam.

Könnyen lehet, hogy a disztribúciónkban található ffmpegben nincs bent ez a könyvtár és saját ffmpeget kell fordítanunk.

A stabilizálás két lépésből áll, először csak megvizsgálja a videót a program és egy transforms.trf fájlban gyűjti össze az adatokat, a második lépesben e fájlt felhasználva történik a tényleges stabilizálás:

```
ffmpeg -i input.mov -vcodec libx264 -acodec aac -vf vidstabdetect output.mkv
ffmpeg -i input.mov -vcodec libx264 -acodec aac -vf vidstabtransform output.mkv
```

Eredeti videó

Nem túlzottan remeg, de teljes képernyőn azért jól látszik, hogy nem használtam állványt.



Stabilizált videó



Egymás mellett a két videó teljes méretben



Egymás mellett a két videó fél méretben



 