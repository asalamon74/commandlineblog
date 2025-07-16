---
layout: post
title: 'mkvpropedit'
excerpt: 'mkvpropedit'
permalink: /2025/07/16/mkvpropedit
categories: 
- mkv
- matroska
- mkvtoolnix
---

A [mediainfo](/2014/06/09/mediainfo_dv_datum) paranccsal kiolvashatunk
adatokat egy mkv fájlból, ha módosítani szeretnénk valamit, az
[mkvpropedit](https://mkvtoolnix.download/doc/mkvpropedit.html) segíthet.

Ha például egy film címét szeretnénk megváltoztatni, a következőképpen 
tehetjük meg:

```
$ mediainfo film.mkv | grep 'Movie name'
Movie name                               : FILM
$ mkvpropedit film.mkv --edit info --set "title=uj cim"
The file is being analyzed.
The changes are written to the file.
Done.
$  mediainfo film.mkv | grep 'Movie name'
Movie name                               : uj cim
```

