---
layout: post
title: 'pipe viewer'
permalink: /2010/02/18/pipe_viewer
post_id: 1697490
categories: 
- pipe
- pv
---

A parancsor használatának egyik hátránya, hogy gyakran nem kapunk visszajelzést arról, hogy az éppen elindított parancs várhatóan mennyi ideig fog futni. Néhány időigényesebb programban van természetesen visszajelzést, de ez nem általános. 
Kihasználva azt, hogy a bonyolultabb parancsokat valószínűleg úgyis pipe-okkal kapcsoljuk össze, használhatjuk a 
[pv](http://www.ivarch.com/programs/pv.shtml) ( pipe viewer ) programot, hogy vizuális visszajelzést kapjunk a futó programunkról. 
Vegyünk egy egyszerű példát, tömörítsünk össze egy nagyméretű fájlt: 
```
gzip nagy.pgn
``` 
Először is vegyük a fentivel megegyező ( leszámítva, hogy megmarad az eredeti tömörítetlen fájl is ) ám a pipe-okat jobban kiemelő formát: 
```
cat nagy.pgn | gzip -c > nagy.gz
``` 
Ha a pv programnak egy fájlnevet adunk paraméternek, akkor a standard outputra másolja a fájl tartalmát, így könnyen lecserélhetjük a cat parancsot: 
```
pv nagy.pgn | gzip -c > nagy.gz
``` 
A pipe viewer segítségével folyamatos információt kapunk arról, hol tartunk a tömörítésben: 
![](/assets/pipe_viewer_1.png)  
 Egy bonyolultabb példában több 
```
pv
```
-t is használhatunk. Az előző példát kibővíthetjük úgy, hogy necsak az input fájl olvasásának sebességéről kapjuk információt, hanem az output írási sebességéről is: 
```
pv -cN pgn nagy.pgn | gzip -c | pv -cN gz > nagy.gz
``` 
Egyrészt kihasználtuk azt, hogy ha 
```
pv
```
 nem kap fájlnevet paraméterként akkor a standard inputot másolja a standard outputra, másrészt elneveztük ( 
```
-N
```
 kapcsoló ) a két pv-t. A 
```
-c
```
 kapcsoló a cursor pozícionálását befolyásolja, 
```
-N
```
 használatakor érdemes használni. 
Az eredmény a következő képen látszik: 
![](/assets/pipe_viewer_2.png) 
  
 Látható, hogy mivel a második pv standard inputról olvassa az adatokat, nem tudhatja, hogy mennyi adat jön még, így ott nincs információ a várható befejezési időről.