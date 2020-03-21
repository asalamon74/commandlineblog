---
layout: post
title: 'pbcopy pbpaste'
permalink: /2018/08/26/pbcopy_pbpaste
post_id: 14201313
categories: 
- mac
- macos
- xclip
- pbcopy
- pbpaste
---

Korábban írtam már az 
[xclip](/2013/07/28/xclip) parancsról, amivel parancssorból kezelhetjük a clipboardot, ha Mac OS alatt van szükségünk erre, akkor a pbcopy pbpaste párost használhatjuk:

```
$ echo 'alma' | pbcopy

 $ echo $(pbpaste)

alma
```