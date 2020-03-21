---
layout: post
title: 'alias kikerülése'
permalink: https://commandline.blog.hu/2012/10/06/alias_kikerulese
post_id: 4822822
categories: 
- alias
---

Nagyon kényelmes az aliasok használata ( egy 
[feh-es példát](http://commandline.blog.hu/2012/06/15/alias_787) én is mutattam már ), viszont időnként hasznos, ha a parancs eredeti változatát tudjuk futtatni az aliasolt helyett. Egyetlen plusz karakterre van szükségünk bash alatt:

```
\parancs
```

A linkelt példában

```
feh -Fd *.jpg
```

használja az alias-t,

```
\feh -Fd *.jpg
```

pedig nem.