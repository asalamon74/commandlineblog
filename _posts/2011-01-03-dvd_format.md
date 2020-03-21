---
layout: post
title: 'dvd format'
permalink: https://commandline.blog.hu/2011/01/03/dvd_format
post_id: 2545710
categories: 
- dvd
- format
- dvd_rw_tools
---

Bár a legtöbb DVD író program képes automatikusan letörölni írás előtt az újraírható DVD lemezeket, időnként szükség lehet arra, hogy egy újraírható lemezt formatáljunk: 
```
dvd+rw-format -force=full /dev/sr0
``` 
Persze 
```
/dev/sr0
```
  helyett mindenki a saját DVD-írójának megfelelő eszköz címét használja! 
A parancs a 
[dvd+rw-tools](http://fy.chalmers.se/~appro/linux/DVD+RW/) csomag része, a név ne zavarjon meg senkit, dvd-rw lemezeket is rendesen kezel.