---
layout: post
title: 'DTS konvertálása AC3-ra'
permalink: https://commandline.blog.hu/2011/06/27/dts_konvertalasa_ac3_ra
post_id: 3015611
categories: 
- ffmpeg
- ac3
- mkvtoolnix
- dt3
---

A 
[DTS kodek](http://en.wikipedia.org/wiki/DTS_%28sound_system%29#DTS_audio_codec) egyik hátránya, hogy elég sok hardveres lejátszó nem képes (inkább jogi/anyagi és nem technikai okoból) lejátszani az így kódolt hangsávot. A következő módszerrel konvertálhatjuk át egy film DTS audióját AC3-ra, amit már nagyobb eséllyel tudunk lejátszani: 
```
mkvextract tracks film_dts.mkv 2:audio.dts
 ffmpeg -i audio.dts -ab 256k audio.ac3
 mkvmerge -o film_ac3.mkv -A film_dts.mkv audio.ac3
``` 
Először kivágjuk az audiósávot (példában ez a 2. track), ezután átkonvertáljuk ac3 formátumba, végül pedig az eredeti film és az új audió track segítségével elkészítjük az új fájlt. A módszer előnye, hogy a videósávot nem konvertáljuk újra.