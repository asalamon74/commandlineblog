---
layout: post
title: 'linuxbrew'
permalink: /2018/11/24/linuxbrew
post_id: 14229049
categories: 
- homebrew
- linuxbrew
---

A Mac OS-en elérhető 
[homebrew](/2018/09/08/homebrew) linuxos forkja a 
[Linuxbrew](http://linuxbrew.sh/). Használatával Linuxra is pont úgy installálhatunk fel programokat mint Mac OS-re. Elsőre kevésbé tűnik hasznosnak, hiszen minden Linux disztribúciónak van saját csomagkezelője, de elég sokszor előfordul, hogy egy csomag kimarad a gyári csomagok közül és linuxbrew-val egyszerűen installálható.

Például Mageia disztróra elég nehéz feltenni shellcheck-et, de linuxbrew-val ez csak egy mozdulat:

```
$ brew install shellcheck
```