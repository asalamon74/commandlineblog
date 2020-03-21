---
layout: post
title: 'pdf jelszóvédelem'
permalink: /2015/11/20/pdf_jelszovedelem
post_id: 8079504
categories: 
- jelszó
- pdf
- pdftk
- ssconvert
---

Jelszóval védhetjük pdf fájljainkat 
[pdftk](http://commandline.blog.hu/2012/02/03/pdftk) segítségével:

```
echo 'titok' > titok.txt
ssconvert titok.{txt,pdf}
pdftk titok.pdf output titok_jelszo.pdf user_pw 1234
```

A példában előszöt titok.pdf fájlt készítettem (
[ssconverttel](http://commandline.blog.hu/2012/10/09/ssconvert)), majd az 1234 jelszót állítottam be.

Ha nem szeretnénk a parancssorba begépelni a jelszót (pl. mert bash history-ba bekerülne), akkor lehetőség van erre is:

```
pdftk titok.pdf output titok_jelszo.pdf user_pw PROMPT
```

A PROMPT hatására pdftk nem a parancssorból veszi a jelszót, hanem megkérdezi a titkosítás előtt. Fontos, hogy PROMPT-ot csupa nagybetűvel írjuk, user_pw prompt hatására létrejön a pdf aminek jelszava prompt.