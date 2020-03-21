---
layout: post
title: 'Hibás szimbolikus linkek'
permalink: /2015/09/08/hibas_szimbolikus_linkek
post_id: 7757652
categories: 
- szimbolikus_link
---

Nagyon hasznosnak tartom a 
[szimbolikus linkeket](http://commandline.blog.hu/2011/07/27/szimbolikus_link_modositasa), de ha letöröljük a fájlt amire mutatnak, akkor semmilyen hibajelzést nem kapunk, vagyis ha nem figyelünk egy idő után elszaporodnak a hibás szimbolikus linkek. Legegyszerűbb a következő módon kereshetjük meg a hibás linkeket:

```
$ find . -type l -xtype l
```

Ha valakit részletesebben érdekel, 
[itt](http://unix.stackexchange.com/q/34248/1228) lehet bővebben olvasni a lehetséges keresési módszerek előnyeiről, hátrányairól.