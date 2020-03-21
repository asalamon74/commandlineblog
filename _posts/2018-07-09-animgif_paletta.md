---
layout: post
title: 'animgif paletta'
permalink: https://commandline.blog.hu/2018/07/09/animgif_paletta
post_id: 14100169
categories: 
- animgif
- ffmpeg
- gifsicle
---

Írtam már egyszer korábban az 
[animgif gyártásáról](https://commandline.blog.hu/2013/05/23/animgif_890), de amikor legutóbb akartam használni az ott leírt módszert, igen csúnya lett az animgif. Egy animgifben csak 256 különböző lehet minden képben és ffmpeg alapesetben ugyanazt a palettát használja, függetlenül a videó színvilágától. Jobb eredményt lehet elérni, ha külön palettát készítünk a videó alapján:

```
ffmpeg -i input.mkv -vf "scale=320:-1:flags=lanczos,fps=25,palettegen" -y palette.png 
ffmpeg -i input.mkv -i palette.png -lavfi "scale=320:-1:flags=lanczos,fps=25 [x]; [x][1:v]paletteuse" -y output.gif
gifsicle -i output.gif -O3 -o output_opt.gif
```

Az első parancsban (a többi filter mellett) a palettegen-t használjuk, ez egy 16x16 pixeles képet gyárt (palette.png) ami az optimális paletta színeit tartalmazza. Ezt használja fel a második parancs az animgif gyártásához a paletteuse filterrel. A harmadik parancs az animgifet optimalizálja gifsicle segítségével.