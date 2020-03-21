---
layout: post
title: 'DVD iso lemezre írása'
permalink: https://commandline.blog.hu/2011/01/09/dvd_iso_lemezre_irasa
post_id: 2546157
categories: 
- dvd
- iso
- genisoimage
- growisofs
---

Bár már többször írtam arról, miként tudunk dvdauthor és genisoimage segítségével iso fájlt gyártani, de valamiért azt elfelejtettem leírni, miként tudjuk ezt parancssorból lemezre írni. Én a következő parancsot használom:  
```
growisofs -dvd-compat -Z /dev/sr0=film.iso
``` 
A
```
/dev/sr0
```
 helyett értelemszerűen a saját DVD-író eszköz címét kell írni. A 
```
-dvd-compat
```
 kapcsoló nem feltétlenül kell, de nekem javította az asztali DVD lejátszóval való kompatibilitást.