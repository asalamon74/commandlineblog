---
layout: post
title: 'xrandr --panning'
permalink: https://commandline.blog.hu/2013/11/20/xrandr_--panning
post_id: 5644987
categories: 
- xrandr
---

A laptopom képernyőjének felbontása 1366x768, ami a legtöbb esetben elegendő ( most elegánsan ugorjuk át, hogy manapság már a legtöbb mobiltelefon felbontása is nagyobb ). Van azonban pár program ami nagyobb felbontást vár el, így az ablakok alja lelóg.

Talán a legegyszerűbb 
[xrandr](http://commandline.blog.hu/2013/05/03/xrandr) segítségével megoldani a problémát:

```
xrandr --output LVDS --panning 1366x1024
```

Ezután egy 1366x1024 pixeles virtuális képernyőn scrollozhatunk fel/le elég könnyen. A visszaállítás sem bonyolult:

```
xrandr --output LVDS --panning 1366x768
```