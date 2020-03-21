---
layout: post
title: 'dvd vágás újrakódolás nélkül'
permalink: https://commandline.blog.hu/2010/04/14/dvd_vagas_ujrakodolas_nelkul
post_id: 1902205
categories: 
- dvd
- genisoimage
- dvdauthor
---

Egy 
[korábbi bejegyzésben](http://commandline.blog.hu/2010/03/05/dvdauthor) leírtam, miként tudunk dvdauthor segítségével egy vob fájlból pár lépéssel menü nélküli DVD-t írni. Egy 
[későbbi bejegyzésben](http://commandline.blog.hu/2010/03/17/process_helyettesites) a vob fájl mpeg-re konvertálásának egy hatékonyabb változatáról is írtam. 
Most egy olyan példát mutatok, ahol dvdauthor-t XML fájl segítségével konfiguráljuk. A cél az, hogy egy vob fájlból úgy írjunk menü nélküli DVD-t, hogy lehetőségünk legyen fejezeteket definiálni, illetve az eredeti DVD egyes részeit kihagyni. Rögtön felmerülhet a kérdés, mi értelme ennek. Nos, gyári DVD-ből kiindulva semmi (illetve önjelölt rendezők újravághatják a filmeket), de ha pl. családi videonkat másoljuk át videokazettáról DVD-felvevő segítségével, akkor lszükség lehet rá. 
Persze mindig van lehetőségünk arra, hogy a hasznos részeket, fejezeteket kijelölve újrakódoljuk a filmet, de az itt leírt megoldásnál nincs szükség újrakódolásra, ami előnyös lehet. 
A 
```
dvdauthor.xml
```
 fájl tartalma a következő: 
```
<dvdauthor>
  <vmgm />
  <titleset>
   <titles>
    <video format="pal" aspect="4:3" />
    <pgc>
     <vob file="mozi.mpg">
       <cell start="0:00:02" end="1:36:45" chapter="yes"/>
       <cell start="1:36:45" end="2:17:15" chapter="yes"/>
       <cell start="2:17:15" end="2:22:21" chapter="yes"/>
       <cell start="2:22:24" end="2:32:04" chapter="yes"/>
       <cell start="2:32:21" end="3:17:20" chapter="yes"/>
     </vob>
    </pgc>
   </titles>
  </titleset>
 </dvdauthor>
``` 
Az egyes fejezetek határait óra:perc:másodperc formátumban adhatjuk meg. Jól látható, hogy több helyek kivágtunk néhány másodpercet. 
A fenti 
```
dvdauthor.xml
```
-t felhasználva a következő módon készíthetünk iso fájlt: 
```
dvdauthor -o dvddir -x dvdauthor.xml
 genisoimage -o mozi.iso -dvd-video dvddir/
```
  