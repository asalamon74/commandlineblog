---
layout: post
title: 'mms rögzítése'
permalink: https://commandline.blog.hu/2011/03/03/mms_rogzitese
post_id: 2704503
categories: 
- mms
- mplayer
---

Az 
[mms](http://en.wikipedia.org/wiki/Microsoft_Media_Server) protokollal továbbított streamelt videót nemcsak nézhetjük, hanem rögzíthetjük is 
[mplayer](http://www.mplayerhq.hu/) segítségével: 
```
mplayer -dumpstream mms://akarmi.szerver.hu/video -dumpfile stream.asf
```