---
layout: post
title: 'diff + process helyettesítés'
permalink: /2011/09/07/diff_process_helyettesites
post_id: 3199586
categories: 
- process
- diff
- exiftool
---

Ha a 
[diff](/2011/09/04/diff_1) segítségével két fájlt szeretnénk összehasonlítani, akkor könnyű dolgunk van, de ha két parancs eredményét kell összehasonlítani akkor már nehezebb a helyzet. Én azt vettem észre, ilyenkor a többség két ideiglenes fájl készít, és azokat hasonlítja össze. Tegyünk fel, két fényképet készítettünk, és össze szeretnénk vetni exiftool segítségével a felvételek paramétereit: 
```
exiftool virag-0000.dng > v0.txt
 exiftool virag-0001.dng > v1.txt
 diff v0.txt v1.txt
``` 
Ehelyett sokkal egyszerűbb 
[process helyettesítést](/2010/03/17/process_helyettesites) alkalmazni: 
```
diff <(exiftool virag-0000.dng) <(exiftool virag-0001.dng)
``` 
Az eredmény mindkét esetben valami ehhez hasonló: 
```
73c73
 < Preview Image Length            : 13585
 ---
 > Preview Image Length            : 13407
 77c77
 < Time                            : 09:09:56
 ---
 > Time                            : 09:12:27
 101c101
 < Camera Temperature              : 26 C
 ---
 > Camera Temperature              : 29 C
```
   
 