---
layout: post
title: 'ebook jpg fájlokból'
permalink: /2014/01/01/ebook_jpg_fajlokbol
post_id: 5719000
categories: 
- jpeg
- jpg
- calibre
- epub
---

A nemrég indult 
[http://ebooks.stackexchange.com/](http://ebooks.stackexchange.com/) oldalon tette fel valaki azt a 
[kérdést](http://ebooks.stackexchange.com/q/279/91), hogy miként lehet jpeg képekből epub fájlt gyártani parancssor használatával. A 
[következő](http://ebooks.stackexchange.com/a/303/91) 2 soros scripet készítettem:

```
for i in *.jpg; do echo \![$i]\($i\); done > alljpgs.txt ebook-convert alljpgs.txt alljpgs.epub --formatting-type markdown
```

Valamiért nem sikerült 1 soros megoldást adnom, pedig próbálkoztam 
[process helyettesítéssel](/2010/03/17/process_helyettesites). Ha valaki tud 1 soros megoldást, kérem írja meg!