---
layout: post
title: 'bash zárójeles kiegészítés'
permalink: /2010/04/20/bash_zarojeles_kiegeszites
post_id: 1909050
categories: 
- kiegészítés
- bash
- zárójeles
---

A bash zárójeles kiegészítése (bash expansion) egy ügyes lehetőség, melyet akkor érdemes használnunk, ha a parancssorba több hasonló paramétert szeretnénk írni. 
Tegyük fel létre szeretnénk hozni 3 fájlt: 
```
touch alma_20100420.txt banán_20100420.txt citrom_20100420.txt
``` 
Látható, hogy bár a fájlnevek eleje különbözik, a végük teljesen azonos. A 
```
_20100420.txt
```
 rész többszöri kiírása felesleges, ráadásul a hibázásra is lehetőséget ad. Ehelyett a fenti parancsot a következő formában is írhatjuk: 
```
touch {alma,banán,citrom}_20100420.txt
``` 
 Ez a forma láthatóan tömörebb, nem kell megismételni a közös részt. 
A kapcsos zárójelek akár egymásba is ágyazhatóak: 
```
touch {alma,banán,citrom{1,2,3}}_20100420.txt
``` 
hatására a következő fájlok jönnek létre:```
alma_20100420.txt, banán_20100420.txt, citrom1_20100420.txt, citrom2_20100420.txt, citrom3_20100420.txt
``` 
 