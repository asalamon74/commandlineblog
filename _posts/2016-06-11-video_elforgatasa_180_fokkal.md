---
layout: post
title: 'Videó elforgatása 180 fokkal'
permalink: /2016/06/11/video_elforgatasa_180_fokkal
post_id: 8797322
categories: 
- video
- ffmpeg
---

Kiderült, hogy az emberi kreativitás határtalan, nemcsak 
[vertikálisan](/2015/10/07/video_elforgatasa)lehet rosszul tartani egy telefont, ha videózik az ember.

Ha fejjel lefelé sikerül felvenni, akkor így lehet visszaforgatni:

```
ffmpeg -i input.mp4 -vf "vflip,hflip" -vcodec libx264 -b:v 10000k output.mp4
```