---
layout: post
title: 'fzf --preview'
excerpt: 'fzf --preview'
permalink: /2020/06/03/fzf_preview
categories: []
---

Írtam már [fzf](/2016/10/08/fzf_840)ről, de nemrég egy igen hasznos
funkcióját fedeztem fel. A `--preview` kapcsolóval egy osztott
képernyőn bal oldalon az input adatokat láthatjuk, jobb oldalon egy
tetszőleges parancs outputját amelynek átadtuk az egyik input adatot.

A következő példa sokkal jobban bemutatja mint a magyarázatom:

```
$ bat --list-themes | fzf --preview="bat --theme={} --color=always
atom.xml"
```

![bat_fzf](/assets/bat_fzf.gif)

