---
layout: post
title: 'szöveg képpé alakítása'
permalink: https://commandline.blog.hu/2010/12/09/szoveg_keppe_alakitasa
post_id: 2501899
categories: 
- text
- convert
- imagemagick
---

A már többször említett 
[ImageMagick](http://www.imagemagick.org/) segítségével könnyen készíthetünk feliratot tartalmazó képeket. 
```
convert -background none -geometry +0+0 -fill \#ffffff -pointsize 36 label:"alma őű" -set label '' felirat.png
``` 
A fenti utasítás hatására átlátszó háttér előtt fehér betűkkel az alma őű felirat jelenik meg. A következő képen látható, hogy a magyar ékezetes betűket is rendesen kezeli a program: 
![](http://commandline.blog.hu/media/image/felirat.png) 
  
  
Ha több soros szöveget szeretnénk, akkor érdemes egy szövegfájlt készíteni, és a következő módon konvertálni: 
```
convert -background none -geometry +0+0 -fill \#ffffff -pointsize 36 label:"`cat felirat.txt`" -set label '' felirat.png
```