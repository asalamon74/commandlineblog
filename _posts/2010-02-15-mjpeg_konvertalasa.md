---
layout: post
title: 'MJPEG konvertálása'
permalink: https://commandline.blog.hu/2010/02/15/mjpeg_konvertalasa
post_id: 1692476
categories: 
- avi
- ffmpeg
- pentax
- k_x
- transcode
- h264
---

Egyre több digitális tükörreflexes fényképezőgéppel lehet normális minőségű videófilmet készíteni. A fényképezőgépek többnyire MJPEG kodeket használnak, vagyis némileg leegszerűsítve minden egyes képkocka egy külön JPEG. Bár az MJPEG-nek vannak előnyei, nagy hátránya, hogy nem túl hatékony. 
A következő példában a Pentax K-X által készített videót konvertáljuk át valami használhatóbb formátumba. A Pentax által készített videóról a következőket érdemes tudni: 
* felbontás: 1280x720
     
* 24 fps
     
* Bitráta kb. 40000 kbps (ez függ a beállított minőségtől, felvételtől)
     
* hang: tömörítetlen pcm, 512 kbps
     
* Weben többen panaszkodnak, hogy nem minden szoftver nyitja meg, ami elvileg támogatja az MJPEG kodeket. (mind később látjuk, nekem ilyen gondom nem volt) 
A cél a következő: 
* Felbontást nem változtatjuk
     
* 24 fps-hez sem nyúlunk (Ha PAL DVD-t készítenénk, akkor érdemes lenne 25 fps-re konvertálni, annak minden nyűgével együtt)
     
* h264 kodeket használunk
     
* hangot mp3-ba konvertáljuk (a default 128 kbps jó lesz). 
Az egyik legjobb Linux alatt elérhető parancssoros konvertert ( 
[transcode](http://tcforge.berlios.de/) ) használva: 
```
transcode -i input.avi -y ffmpeg,tcaud -F h264 -o output.avi
``` 
A paraméterek magyarázata: 
* ```
-i input.avi
```
     Input fájl. Szerencsére transcode felismeri a formátumot, ffmpeg import modult használva fel is tudja dolgozni minden gond nélkül.
     
* ```
-y ffmpeg,tcaud
```
     Export modulok megadása. A videót ffmpeg export modullal, az audiót tcaud export modullal fogjuk elkészíteni.
     
* ```
-F h264
```
 kodek kiválasztása. ffmpeg számtalan kodeket ismer, ezek közül választjuk a h264-et.
* ```
-o output.avi
```
 output fájl.Nyilván a finomhangolással még rengeteg időt el lehetne tölteni. 
  
  
 