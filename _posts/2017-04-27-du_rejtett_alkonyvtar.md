---
layout: post
title: 'du rejtett alkönyvtár'
permalink: /2017/04/27/du_rejtett_alkonyvtar
post_id: 12456153
categories: 
- du
---

Egy alkönyvtáram helyfoglalását akartam ellenőrizni 
[du](http://commandline.blog.hu/2010/07/31/du_1)-val, de valahogy hiányzott néhány gigabájt.

Az általam többynire használt

```
du -ms *
```

sajnos teljesen ignorálja a rejtett alkönyvtárakat. Ha azokról is adatra lenne szükségünk, akkor a következő módon kell du-t meghívni:

```
du -ms .[!.]* *
```