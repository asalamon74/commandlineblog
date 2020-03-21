---
layout: post
title: 'xbacklight'
permalink: /2012/07/25/xbacklight
post_id: 4670510
categories: 
- xbacklight
- randr
---

A 
[RandR](http://en.wikipedia.org/wiki/RandR)-re épülő 
[xbacklight](http://cgit.freedesktop.org/xorg/app/xbacklight/) segítségével parancssorból tudjuk a monitor fényerejét állítani, illetve a beállított fényerőt lekérdezni:

```
$ xbacklight -set 100
$ xbacklight -get
100.000000
$ xbacklight -set 80
$ xbacklight -get
79.166667
```

Az értékekek százalékot jelentenek.