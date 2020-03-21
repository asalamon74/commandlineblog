---
layout: post
title: 'GNU parallel - több számítógép'
permalink: https://commandline.blog.hu/2012/07/31/gnu_parallel_tobb_szamitogep
post_id: 4682459
categories: 
- convert
- parallel
---

[Dicsértem](http://commandline.blog.hu/2012/05/03/gnu_parallel) már 
[GNU parallel](http://www.gnu.org/software/parallel/)t, a korábbi példákban csak egyetlen számítógépet használtam. Parallel képes arra is, hogy az elvégzendő feladatot több számítógép között ossza szét. Itt most egy elég speciális esetet mutatok be, valójában nem osztjuk szét a feladatot, hanem inkább átadjuk egy gyorsabb számítógépnek.

Vegyünk egy alkönyvtárat, ahol sok jpg fájl van, ezeket szeretnénk png-re konvertálni és közben ( csak hogy lassabb legyen ) még egy kicsit életleníteni. A következő parancsot futtatjuk egy fájlra:

```
convert alma.jpg -gaussian-blur 5x5 alma.png
```

Parallel segítségével az alkönyvtár összes jpeg fájljának feldolgozása:

```
find . -name "*.jpg" | parallel convert {} -gaussian-blur 5x5 {.}.png
```

A lassú számítógépen ez 12 perc 17 másodpercig fut, a gyors számítógépen 48 másodpercig.

Felmerülhet a kérdés, hogyan fértem hozzá a laptopomnál 15-ször gyorsabb számítógéphez. A válasz egyszerű, a példában a laptop a gyors gép, egy 15-ször lassabb géphez fértem hozzá.

Ha a lassú gépen dolgozunk, akkor alapesetben az input fájlokat össze kell csomagolnunk, átmásolnunk a gyors gépre, ott ugyanazt a scriptet lefuttatni, majd a végeredményt visszamásolni. Parallel mindezt megteszi helyettünk:

```
find . -name "*.jpg" | parallel -S user@gyors.akarmi.hu --trc {.}.png convert {} -gaussian-blur 5x5 {.}.png
```

A -S kapcsoló után kell megadnunk a gépek listáját, melyek elvégzik a feladatot. Itt egyetlen egy gépet adtam meg. A --trc a transfer, return, cleanup rövidítése, hatására az input fájlokat ( jpeg fájlok ) átmásolja parallel a másik gépre, majd a png fájlokat visszamásolja, és a a távoli gépről le is törli.

Több dolog is szükséges ahhoz, hogy a fenti parancs működjön:

* Minden gépen fel kell installálnunk parallelt.


* Azt a programot is fel kell installálnunk, amit a parallel meghív ( példában: convert ),


* [Jelszó nélkül](http://commandline.blog.hu/2012/07/27/ssh_jelszo_nelkul) be kell tudnunk lépni a másik gépre ssh-val.

A parancs futtatásához 2 perc 20 másodperc kell, ami persze lényegesen több a 48 másodpercnél ( a fájlok másolása, a parancsok ütemezése elvesz némi időt ), de sokkal gyorsabb a kiinduló 12 perc 17 másodpercnél.