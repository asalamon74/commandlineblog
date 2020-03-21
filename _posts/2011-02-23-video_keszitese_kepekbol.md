---
layout: post
title: 'Videó készítése képekből'
permalink: /2011/02/23/video_keszitese_kepekbol
post_id: 2682479
categories: 
- mkv
- jpeg
- ffmpeg
---

Állóképeket összefűzve készíthetünk mozgóképet 
[ffmpeg](http://www.ffmpeg.org/) használatával: 
```
ffmpeg -r 4 -i kep_%02d.jpg -vcodec libx264 -vpre normal -b 1800k -aspect 3:2 video.mkv
``` 
A kapcsolók egy része a videó kódolását határozza meg (
```
-vcodec, -vpre, -b
```
 ) ezekkel itt most nem foglalkozok részletesebben. A többi kapcsoló jelentése: 
```
-i kep_%02.jpg
``` 
A szokásos használattal ellentétben itt nem egy input fájlunk van, hanem sok (ahány képet szeretnénk összefűzni). A kapcsoló hatására a 
```
kep_00.jpg, kep_01.jpg, kep_02.jpg
```
,... fájlokat fogja használni ffmpeg. 
```
-r 4
```A -i kapcsoló előtt szereplő -r kapcsolóval azt határozhatjuk meg, milyen gyorsan cserélődjenek a fényképek. A másodpercenként használt fényképek számát adhatjuk itt meg. 
```
-aspect 3:2
``` 
A képarányt adhatjuk itt meg. A gyakorlatban a 3:2 helyett persze inkább 4:3 vagy 16:9 a használatos. 
Végül egy példa videó, amit a fenti módszerrel készítettem, a képeken elhelyezett számok miatt jól látszik a képek cseréje: 
  
 
 