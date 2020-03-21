---
layout: post
title: 'ffmpeg osztott képernyő'
permalink: /2017/01/04/ffmpeg_osztott_kepernyo
post_id: 12085429
categories: 
- ffmpeg
---

Az 
[előző](http://commandline.blog.hu/2017/01/01/videostabilizalas) bejegyzésemben szerepelt két osztott képernyős felvétel, amit ffmpeggel készítettem.

Az első felvételnél két videót ragasztottam egymás mellé, így a két 1920x1080-as videóból egy 3840x1080-as videót kaptam:

```
ffmpeg -i bal.mkv -i jobb.mkv -filter_complex "[0:v]pad=iw*2:ih[bg]; [bg][1:v]overlay=w" output.mkv
```



A második esetben a bal oldali videó bal felét a jobb oldali videó jobb felével ragasztottam össze és egy néhány pixeles fekete csíkkal emeltem ki az összeillesztés helyét. Az eredmény így egy 1920x1080-as videó:

```
ffmpeg -i bal.mkv -i jobb.mkv -filter_complex "[0:v]crop=iw/2-4:ih:0:0[left]; [1:v]crop=iw/2:ih:ow:0[right]; [left]pad=2*iw+8:ih[bg]; [bg][right]overlay=w" output.mkv
```