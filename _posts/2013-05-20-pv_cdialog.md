---
layout: post
title: 'pv + cdialog'
permalink: https://commandline.blog.hu/2013/05/20/pv_cdialog
post_id: 5305738
categories: 
- pv
- dialog
- cdialog
---

A 
[pv ( pipe viewer )](http://commandline.blog.hu/2010/02/18/pipe_viewer) és a 
[cdialog](http://commandline.blog.hu/2013/05/17/cdialog) együttes használatával elég könnyen tudunk egy hosszú műveletről folyamatos tájékoztatást adni.

A "nyers" pv parancs így néz ki:

```
$ pv nagy.pgn | gzip -c > nagy.gz
```

pv és cdialog összekötve:

```
$ (pv -n nagy.pgn | gzip -c > nagy.gz) 2>&1 | dialog --gauge "Tömörítés..." 10 70
```

Az eredmény egy ehhez hasonló dialógusablak:

![pv_dialog.gif](http://m.cdn.blog.hu/co/commandline/image/pv_dialog.gif)