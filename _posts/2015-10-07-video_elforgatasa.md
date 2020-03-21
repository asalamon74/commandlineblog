---
layout: post
title: 'videó elforgatása'
permalink: https://commandline.blog.hu/2015/10/07/video_elforgatasa
post_id: 7920842
categories: 
- ffmpeg
- vertical_video_syndrome
---

Vertikális videót készíteni rettentően értelmetlen ( vonatkozó szakirodalom: 
[itt](https://www.youtube.com/watch?v=Bt9zSfinwFA) ) de sajnos mégis igen elterjedt. Az ilyen videókat (melyeket nem én készítek!) ffmpeggel szoktam visszaforgatni:

```
ffmpeg -i input.mp4 -vf "transpose=1" -vcodec libx264 -b:v 1000k output.mp4
```

A transpose=1 az óramutató járásával megegyező irányban forgat 90 fokot.