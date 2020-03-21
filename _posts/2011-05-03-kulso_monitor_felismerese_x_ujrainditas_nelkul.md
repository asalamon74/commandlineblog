---
layout: post
title: 'Külső monitor felismerése X újraindítás nélkül'
permalink: https://commandline.blog.hu/2011/05/03/kulso_monitor_felismerese_x_ujrainditas_nelkul
post_id: 2869032
categories:  []
---

Bár viszonylag könnyen beállítottam a laptopomon (Mivel ATI kártya van benne ezért ATI Catalyst Control Centerrel), hogy a külső monitort is használja, sajnos csak bootoláskor (pontosabban az X indításakor) detektálta a monitort. Ha később csatlakoztattam, nem ismerte fel automatikusan. Hasonlóan gondot okozott a bootoláskor még csatlakoztatott monitor eltávolítása. 
Némi utánaolvasás után kiderült, az 
[xrandr](http://www.x.org/wiki/Projects/XRandR) parancssoros eszközzel nagyon könnyen rávehetem az X-et, hogy újra megvizsgálja csatlakoztatva van-e a külső monitort, és megfelelő üzemmódra váltson: 
```
xrandr --auto
``` 