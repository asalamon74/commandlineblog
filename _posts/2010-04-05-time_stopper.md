---
layout: post
title: 'time stopper'
permalink: https://commandline.blog.hu/2010/04/05/time_stopper
post_id: 1862836
categories: 
- time
- stopper
---

A 
[time](http://linux.die.net/man/1/time) paranccsal egy program futási idejét tudjuk megmérni. Pl. ha a egy tömörítés idejére vagyunk kíváncsiak: 
```
time gzip nagy.txt
``` 
A time-ot akár (egy igen egyszerű) stopperként is használhatjuk: 
```
time cat
``` 
A stopperórát 
```
CTRL-D
```
 segítségével állíthatjuk le.