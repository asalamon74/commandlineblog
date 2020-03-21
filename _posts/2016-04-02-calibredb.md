---
layout: post
title: 'calibredb'
permalink: https://commandline.blog.hu/2016/04/02/calibredb
post_id: 8553960
categories: 
- calibre
- calibredb
---

A calibre néhány parancssoros eszközéről már írtam 
[korábban](http://commandline.blog.hu/tags/calibre), de ha a könyvadatbázisom kellett karbantartani, akkor eddig mindig elindítottam a GUI-t. Ez elég kényelmetlen, ha egyetlen könyvet akartam csak az adatbázisba tenni.

Szerencsére ez parancssorból sokkal egyszerűbben megy 
[calibredb](https://manual.calibre-ebook.com/generated/en/calibredb.html) használatával:

```
calibredb add konyv.epub
```

Sajnos a 
send to device parancsot nem lehet parancssorból elérni, legalábbis én nem találtam meg.

 

 