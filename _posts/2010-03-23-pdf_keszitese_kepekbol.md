---
layout: post
title: 'pdf készítése képekből'
permalink: https://commandline.blog.hu/2010/03/23/pdf_keszitese_kepekbol
post_id: 1836763
categories: 
- pdf
- convert
- imagemagick
---

A korábban már 
[említett](http://commandline.blog.hu/2010/01/22/imagemagick) 
[imagemagick](http://www.imagemagick.org/) segítségével egyetlen utasítással pdf-et készíthetünk különálló képekből: 
```
convert *.jpg kepek.pdf
``` 
Ha kisebb méretű pdf-et szeretnénk (a képek minőségének romlása árán), használjuk a 
```
-quality
```
 kapcsolót: 
```
convert *.jpg -quality 50 kepek.pdf
```