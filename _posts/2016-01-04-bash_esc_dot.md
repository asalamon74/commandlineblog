---
layout: post
title: 'bash ESC dot'
permalink: /2016/01/04/bash_esc_dot
post_id: 8215804
categories: 
- meta
- bash
- ESC
---

Könnyen felhasználhatjuk az előző parancs paramétereit bash-ban az ESC dot segítségével:

```
$ echo aaaa bbbb cccc dddd
 aaaa bbbb cccc dddd
```

Ha egymás után lenyomjuk az ESC és a pont billentyűket, akkor bash automatikusan a parancssorra másolja az előző parancs utolsó paraméterét (dddd).

A korábbi paramétereket is elérhetjük. 
```
<ESC> 1 <ESC> .
```
az első paramétert (aaaa), 
```
<ESC> 2 <ESC> .
```
 a második paramétert (bbbb) másolja...

Ha a billentyűkombinációt többször egymás után használjuk, akkor a korábbi parancsok paramétereit érjük el. Vagyis pl. 
```
<ESC> . <ESC> .
```
 az utolsó előtti parancs utolsó paraméterét adja vissza.

Több helyen ESC dot helyett META dot-ként hivatkoznak erre. Nekem Meta (vagyis Alt) billentyűvel ez nem igazán működik. Van olyan terminál ahol egyáltalán nem megy, van olyan ahol csak az Alt-. megy.