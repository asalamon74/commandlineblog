---
layout: post
title: 'named pipe'
permalink: /2010/03/08/named_pipe
post_id: 1775484
categories: 
- pipe
- tee
- named
- mplex
---

A dvdauthor parancssoros használatát bemutató 
[bejegyzésben](/2010/03/05/dvdauthor) szerepelt az alábbi kódrészlet: 
```
tcextract -i mozi.vob -t vob -x mpeg2 > mozi.m2v
 tcextract -i mozi.vob -t vob -x ac3 > mozi.ac3 
 mplex -f 8 -o mozi.mpg mozi.m2v mozi.ac3
``` 
 Ha jobban megnézzük, akkor észrevehető, hogy 
```
mozi.vob
```
 fájlt kétszer olvassuk végig. Ez nyilván nem túl hatékony, a mostani bejegyzés célja egy olyan megoldás bemutatása, ahol elég egyszer végigolvasni a fájl. 
(Ha csak egyszer olvassuk végig, akkor nem is feltétlenül kell a DVD-ről a vob fájlt átmásolni a merevlemezre). 
Korábban már többször használtunk pipe-okat (csöveket), most is ezt fogjuk tenni, de a korábbi példákkal ellentétben most 
[named pipe](http://en.wikipedia.org/wiki/Named_pipe)-okra ( másnéven FIFO, magyarul talán elnevezett vagy nevesített cső ) lesz szükségünk: 
```
mkfifo aud.fifo
 mkfifo vid.fifo
 tcextract -i vid.fifo -t vob -x mpeg2 > mozi.m2v &
 tcextract -i aud.fifo -t vob -x ac3 > mozi.ac3 &
 cat mozi.vob | tee vid1.fifo aud1.fifo > /dev/null
 mplex -f 8 -o mozi.mpg mozi.m2v mozi.ac3
 rm aud.fifo vid.fifo
``` 
Először is létrehozunk 2 named pipe-ot az 
[mkfifo](http://people.inf.elte.hu/csa/MAN/HTML/mkfifo.htm) paranccsal, és elindítjuk a háttérben ( & ) a két 
```
tcextract
```
 parancsot, ami az eredeti verzióval szemben nem a 
```
mozi.vob
```
 fájlt, hanem a csöveket olvassa. Adat is kell a csövekbe, ezért 
```
cat
```
 paranccsal olvassuk ki a vob fájlt, a 
[tee](/2010/03/02/tee_4) segítségével pedig egyszerre öntjük bele a kiolvasott adatot a 2 csőbe. Az 
```
mplex
```
 parancs nem változott, a legvégén letöröljük a csöveket.