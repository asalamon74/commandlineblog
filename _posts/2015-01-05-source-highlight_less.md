---
layout: post
title: 'source-highlight + less'
permalink: https://commandline.blog.hu/2015/01/05/source-highlight_less
post_id: 7027831
categories: 
- less
- sourse-highlight
---

A less egyik hiányossága, hogy nem támogatja a syntax highlightot, de külső programmal rávehető erre. A 
[source-hightlight](http://www.gnu.org/software/src-highlite/source-highlight.html) installálása után a következő 2 környezeti változót kell beállítani

```
export LESS=' -R '
export LESSOPEN='| /usr/bin/src-hilite-lesspipe.sh %s'
```

és less már szépen színezi is a fájlokat.

forrás: 
[http://superuser.com/a/71593/8240](http://superuser.com/a/71593/8240)