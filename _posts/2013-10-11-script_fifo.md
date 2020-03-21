---
layout: post
title: 'script + fifo'
permalink: /2013/10/11/script_fifo
post_id: 5562857
categories:  []
---

A 
[nemrég említett](/2013/10/05/script_scriptreplay) script egy másik érdekes használata a következő:

1. terminál:

```
$ mkfifo scriptpipe
$ script -f scriptpipe
```

2. terminál:

```
cat scriptpipe
```

Ezután az 1. terminálban dolgozhatunk tovább, és a 2. terminálban valós időben követhetjük az eseményeket.