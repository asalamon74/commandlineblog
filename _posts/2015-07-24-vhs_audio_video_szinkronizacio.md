---
layout: post
title: 'VHS audio video szinkronizáció'
permalink: /2015/07/24/vhs_audio_video_szinkronizacio
post_id: 7646734
categories: 
- video
- audio
- sync
- mencoder
- VHS
---

Ha VHS-t próbálunk digitalizálni, akkor számomra nem teljesen érthető okokból az audio és a video sáv egymáshoz képest mindenképpen el lesz csúszva. A legjobb amit elértem, hogy az eltérés (nagyjából) konstans, vagyis egy kicsit elcsúsztatva rendben lesz a felvétel.

Ehhez hozzáadva, hogy a szalag elején és végén többnyire lesz egy felesleges rész, én a következő parancsot szoktam használni a digitalizált avi feldolgozásához:

```
mencoder -delay -3.2 -ss 00:56.5 -endpos 58:19 -oac copy -ovc copy -o output.avi input.avi
```

A -delay-nél adom meg az audio és video sáv közti különbséget másodpercben. Az -ss a kezdete, az -endpos a vége az engem érdeklő résznek. A fenti parancs nem kódolja újra a felvételt (-oac copy, -ovc copy) így nagyon gyorsan lefut.

 