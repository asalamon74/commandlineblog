---
layout: post
title: 'DNG tömörítés'
permalink: https://commandline.blog.hu/2015/11/29/dng_tomorites
post_id: 8121962
categories: 
- pentax
- dng
- qimport
---

A Pentax elég régóta támogatja a 
[DNG](https://en.wikipedia.org/wiki/Digital_Negative) fájlformátumot, Többek között nyilván azért, mert a saját PEF formátumukat nem tudták eléggé elterjeszteni. 
[Nagyon sok](http://photo.stackexchange.com/q/762/507) fényképezőgépük képest DNG-be menteni. Eleinte tömörítetlen DNG-t gyártottak, később már veszteségmentesen tömörítettet. Számomra kissé furcsa módon a Q sorozat gépei újra tömörítetlen DNG-be mentenek.

Ha helyet szeretnénk spórolni, akkor a 
[qimport](https://github.com/drougge/qimport) segítségével konvertálhatjuk a tömörítetlen DNG fájlokat tömörített DNG fájlokká. Ha szükséges, akkor a visszafelé konverziót is elvégezhetjük:

```
$ qimport imgp2584.dng imgp2584_compressed.dng
 $ qimport --reverse imgp2584_compressed.dng imgp2584_uncompressed.dng
```

A program JPEG tömörítést használ, de nem kell kétségbeesni, 
[veszteségmentes jpeg](https://en.wikipedia.org/wiki/Lossless_JPEG)ről van itt szó, 
[Huffman-kódolást](https://hu.wikipedia.org/wiki/Huffman-k%C3%B3dol%C3%A1s) használ a program.

Bár a program neve arra utal, hogy a Pentax Q sorozat DNG fájljait tudja kezelni, a kódot megnézve nekem úgy tűnik más (12 bites) DNG fájlokkal is boldogul.