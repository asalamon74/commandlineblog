---
layout: post
title: 'colordiff'
permalink: https://commandline.blog.hu/2012/11/13/colordiff
post_id: 4888046
categories: 
- less
- diff
- colordiff
---

Nagyon sokszor használom a 
[diff](http://commandline.blog.hu/2011/09/04/diff_1) parancsot, de időnként nehéz értelmezni az eredményt, a kacsacsőrök miatt könnyű összekeverni a fájlokat. Másnak is feltűnt ez, így elkészítették a 
[colordiff](http://www.colordiff.org/) programot, ami színkódokkal jelzi, hogy melyik rész melyik fájlhoz tartozik:

```
$ diff file1.txt file2.txt 
2c2
< bbb
---
> bbbb
3a4
> dd
$ colordiff file1.txt file2.txt 
2c2< bbb---
> bbbb3a4> dd
```

Arra kell figyelni még, hogyha less-nek adjuk át az eredményt, akkor a -R kapcsoló is kell, ellenkező esetben less nem mutatja rendesen a színeket:

```
colordiff file1.txt file2.txt | less -R
```