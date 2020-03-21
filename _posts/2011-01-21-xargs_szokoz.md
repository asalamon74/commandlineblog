---
layout: post
title: 'xargs szóköz'
permalink: /2011/01/21/xargs_szokoz
post_id: 2549086
categories: 
- find
- xargs
- whitespace
---

A fájlnevekben szereplő szóközökkel mindig csak baj van. Készítsünk egy scriptet, ami a jpeg fájlokban található 
[exif](http://commandline.blog.hu/2010/05/14/exiftool) információ alapján megnézi, hogy milyen ISO értékekkel fényképeztünk: 
```
find . -name "*.jpg" | xargs -n1 exiftool -m -iso
``` 
A script nagyszerűen működik, egészen addig amíg bele nem szaladunk egy olyan alkönyvtárba, aminek a nevében szóköz van. A gondot az okozza, hogy ugyanaz a szóköz választja el a fájlok neveit, mint az ami az alkönyvtár nevében is szerepel. Ha a fájlneveket elválasztó karaktert lecseréljük ( null karakterre ), akkor már működik a scriptünk: 
```
find . -name "*.jpg" -print0 | xargs -0 -n1 exiftool -m -iso
``` 
Látható, hogy egyrészt find-nak, másrészt xargs-nak is meg kell adni, hogy ne szóközökkel dolgozzon.