---
layout: post
title: 'parancsbehelyettesítés'
permalink: https://commandline.blog.hu/2010/03/14/parancs_behelyettesites
post_id: 1796971
categories: 
- date
- pipe
- parancsbehelyettesítés
---

A korábban már gyakran használt pipe-ok mellett más mód is van rá, hogy egy parancs eredményét egy másik parancsnak átadjuk. A 
```
`
```
 karakter segítségével tudjuk a parancsbehelyettesítést (command substitution) használni. Az 
```
mkdir backup_`date +%Y%m%d`
``` 
hatására lefut a 
```
date
```
 parancs és visszaadja az aktuális nap dátumát 
```
yyyymmdd
```
 formátumban, így a bejegyzés élesítésekor a fenti utasítás az 
```
mkdir backup_20100314
``` 
parancsnak felel meg. 
Bár eredetileg a fent is használt 
```
`
```
 karakterrel lehetett csak a parancsbehelyettesítést használni, egy ideje inkább a 
```
$()
```
 használata javasolt (pl. a könnyebb egymásbaágyazhatóság miatt). Vagyis a 
```
mkdir backup_$(date +%Y%m%d)
``` 
forma is használható.