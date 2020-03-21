---
layout: post
title: 'fallocate'
permalink: /2016/07/05/fallocate
post_id: 8865424
categories: 
- dd
- ext4
- fallocate
---

Az 
[előző bejegyzés](http://commandline.blog.hu/2016/07/02/sparse_fajlok)ben mutattam egy példát arra, hogyan lehet dd-vel lassan "rendes" és gyorsan sparse fájlt gyártani. Nyilván felmerül a kérdés, van-e mód arra, hogy gyorsan gyártsunk rendes fájlt. Számomra kissé meglepő módon van:

```
$ time fallocate -l 1G fallocateg.txt
real    0m0.003s
user    0m0.000s
sys     0m0.000s
$ ls -lsk fallocateg.txt 
1048580 -rw-r--r-- 1 user live 1073741824 Jun 29 20:40 fallocateg.txt
```

A fallocate villámgyorsan működik és nem sparse fájlt hoz létre. Ha jól értem, akkor a trükkje az, valóban lefoglalja a helyet, de nem írja ki a drive-ra a rengeteg 00-t. Nem minden fájlrendszernél működik, pl. ext3 nem elég, ext4 kell neki.