---
layout: post
title: 'Process helyettesítés'
permalink: /2010/03/17/process_helyettesites
post_id: 1796998
categories: 
- helyettesítés
- process
- pipe
- tee
---

 A named pipe 
[bemutatásakor](http://commandline.blog.hu/2010/03/08/named_pipe) a következő példát: 
```
tcextract -i mozi.vob -t vob -x mpeg2 > mozi.m2v
 tcextract -i mozi.vob -t vob -x ac3 > mozi.ac3 
 mplex -f 8 -o mozi.mpg mozi.m2v mozi.ac3
``` 
 átírtam erre az új, hatékonyabb verzióra: 
```
mkfifo aud.fifo
 mkfifo vid.fifo
 tcextract -i vid.fifo -t vob -x mpeg2 > mozi.m2v &
 tcextract -i aud.fifo -t vob -x ac3 > mozi.ac3 &
 cat mozi.vob | tee vid1.fifo aud1.fifo > /dev/null
 mplex -f 8 -o mozi.mpg mozi.m2v mozi.ac3
 rm aud.fifo vid.fifo
``` 
Bár ez az új verzió hatékonyabb, hiszen csak egyszer olvassa végig a 
```
mozi.vob
```
 fájlt, semmiképpen sem nevezhető túl szépnek. Kétszer olyan hosszú mint az előző, és a name pipe létrehozás majd törlés elég feleslegesnek tűnik. 
Szerencsére valóban van egy sokkal tisztább megoldás, a csövek helyett process helyettesítést kell alkalmazni: 
```
cat mozi.vob | tee >(tcextract -t vob -x mpeg2 > mozi.m2v) >(tcextract -t vob -x ac3 > mozi.ac3) > /dev/null
 mplex -f 8 -o mozi.mpg mozi.m2v mozi.ac3
``` 
A 
```
>()
```
 segítségével (nem kell szóköz a zárójel elé!) ügyesen össze tudjuk kötni a 
```
tee
```
 parancsot és a 
```
tcextract
```
 parancsokat (a 
```
-i
```
 kapcsolóra azért nincsen szükség, mert 
```
tcextract
```
 nem fájlból, hanem standard inputról olvas). 
Érdemes még megjegyezni, hogy a process helyettesítés (process substitution) nem összekeverendő a 
[parancsbehelyettesítés](http://commandline.blog.hu/2010/03/14/parancs_behelyettesites)sel (command substitution).