---
layout: post
title: 'gnuplot oszlopdiagram'
permalink: /2011/07/14/gnuplot_oszlopdiagram_1
post_id: 3054203
categories: 
- gnuplot
---

A 
[gnuplot](http://www.gnuplot.info/) egy rendkívül összetett adat- és függvényábrázoló program. Ingyenes, számtalan operációs rendszeren elérhető. Bonyolultságát mutatja az is hogy külön könyvek foglalkoznak vele, és sajnos az is, hogy eleinte elég nehezen konfigurálhatónak tűnik. 
A példában az exiftool segítségével készített 
[statisztikát](/2011/07/11/statisztika_keszitese_exiftool_segitsegevel) szeretném megjeleníteni gnuplot segítségével. A graph.plt fájlban írjuk le mit szeretnénk megjeleníteni: 
```
set xlabel 'focal length'
 set style data histograms
 set style fill solid 1.0 border -1
 set term png
 set output 'graph.png'
 plot 'focal_length_35.txt' using 1:xticlabels(2) notitle
``` 
A sorok jelentése a következő: 
```
set xlabel 'focal length'
``` 
Az x tengelyen megjelenő felirat. 
```
set style data histograms
 set style fill solid 1.0 border -1
``` 
Beállítjuk hogy oszlopdiagramot szeretnénk, és az oszlopok stílusát is megadjuk. 
```
set term png
 set output 'graph.png'
``` 
E két utasítás hatására az eredmény nem a képernyőn jelenik meg, hanem a graph.png fájlban. 
```
plot 'focal_length_35.txt' using 1:xticlabels(2) notitle
``` 
Itt a lényeg, ez a parancs felelős a rajzolásért. A focal_length_35.txt fájl tartalmazza az adatokat, az 1. oszlop a gyakoriságot, a második pedig az x tengely értékeit. 
A konfigurációs fájl elkészítése után már egyszerűen elkőszíthető az ábra: 
```
gnuplot graph.plt
``` 
Az eredmény pedig itt látható: 
 
![](http://commandline.blog.hu/media/image/gnuplot_test1.png) 
 