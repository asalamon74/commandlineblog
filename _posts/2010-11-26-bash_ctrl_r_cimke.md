---
layout: post
title: 'bash ctrl-r címke'
permalink: https://commandline.blog.hu/2010/11/26/bash_ctrl_r_cimke
post_id: 2470927
categories: 
- címke
- bash
---

Korábban 
[írtam](http://commandline.blog.hu/2010/01/28/bash_ctrl_r) róla, miként tudunk 
```
ctrl-r
```
 segítségével könnyen megtalálni egy korábban kiadott parancsot. A módszer egyik nehézsége, hogy nem mindig tudunk olyan rövid könnyen megjegyezhető részletet megjegyezni a parancsból, aminek a használatával gyorsan előhozhatjuk a több napja kiadott utasítást. Egy apró trükk segítségével címkét ragaszthatunk ahhoz az utasításhoz amit később várhatóan még többször szeretnénk használni:```
itt_egy_nagyon hosszú parancs van sok paraméterrel # alma
``` 
A # utáni rész ( 
```
alma
```
 ) nem befolyásolja a futást, de a 
```
ctrl-r
```
 kereséskor könnyen rákereshetünk.