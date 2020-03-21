---
layout: post
title: 'avi index javítás'
permalink: https://commandline.blog.hu/2010/02/12/avi_index_javitas
post_id: 1688314
categories: 
- index
- avi
- mplayer
- mencoder
---

Ha egy avi fájl indexe sérült vagy hiányzik, 
[mplayer](http://www.mplayerhq.hu/)segítségével könnyen lejátszhatjuk: 
```
mplayer -forceidx hibasindex.avi
``` 
Ha meg szeretnénk javítani az indexet, akkor mencoder-t (mplayer encoder) használhatjuk: 
```
mencoder -forceidx hibasindex.avi -o joindex.avi -oac copy -ovc copy
```
  