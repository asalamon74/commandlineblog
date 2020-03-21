---
layout: post
title: 'bash for ciklus'
permalink: https://commandline.blog.hu/2010/05/17/bash_for_ciklus
post_id: 2003859
categories: 
- for
- bash
---

Elég furcsa, de úgy látom sokan nem szeretik használni a bash for ciklusát, talán a nehézkes szintaktika miatt. A következő példák remélhetően segítik a megértést: 
```
[gep]$ for i in 1; do echo $i; done
 1
``` 
```
[gep]$ for i in 1 3 5; do echo $i; done
 1
 3
 5
``` 
```
[gep]$ for i in `seq 1 2 7`; do echo $i; done
 1
 3
 5
 7
``` 
```
[gep]$ for i in 1 3 5; do echo teszt_$i; done
 teszt_1
 teszt_3
 teszt_5
``` 
```
[gep]$ for i in *.jpg; do echo $i; done
 alma.jpg
 korte.jpg
``` 
Ha valami nem megy, akkor többnyire a pontosvesszőkkel van a gond.Egy életszerűbb (és némileg bonyolultabb) példa található 
[ebben](http://commandline.blog.hu/2010/01/22/imagemagick) a korábbi bejegyzésben.