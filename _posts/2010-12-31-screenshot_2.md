---
layout: post
title: 'Screenshot'
permalink: https://commandline.blog.hu/2010/12/31/screenshot_2
post_id: 2544026
categories: 
- screenshot
- mplayer
---

Ha egy videófájlból szeretnénk screenshotokat elmenteni, akkor 
[mplayer](http://www.mplayerhq.hu/) segítségével könnyen megtehetjük: 
```
mplayer -vf screenshot film.mpg
``` 
Ezután a megfelelő pillanatban az 
```
s
```
 billentyű lenyomásával készíthetjük el a screenshotokat, melyeket 
```
shot0001.png, shot0002.png,...
```
 néven ment el a program.