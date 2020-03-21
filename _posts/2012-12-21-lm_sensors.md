---
layout: post
title: 'lm_sensors'
permalink: https://commandline.blog.hu/2012/12/21/lm_sensors
post_id: 4975835
categories: 
- szenzor
- lm_sensors
---

A mai számítógépekben meglepően sok szenzor található, az ezek által kiolvasott ( többnyire hőmérséklet ) értékeket az 
[lm_sensors](http://www.lm-sensors.org/) használatával olvashatjuk ki.

Először is detektálnunk kell a szenzorokat:

```
sensors-detect
```

A program ( amit root joggal kell futtatni ) elég sok ijesztő kérdést tesz fel, mindegyikre igennel válaszoltam.

Ezután ( de az sem árt, ha bootolunk egyet) már kiolvashatjuk az adatokat:

```
$ sensors
acpitz-virtual-0
Adapter: Virtual device
temp1:        +62.0°C  (crit = +108.0°C)
temp2:        +46.0°C  (crit = +100.0°C)
temp3:        +49.0°C  (crit = +103.0°C)
temp4:        +48.0°C  (crit = +105.0°C)
temp5:        +27.2°C  (crit = +103.0°C)
temp6:        +45.0°C  (crit = +110.0°C)
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +49.0°C  (high = +100.0°C, crit = +100.0°C)
Core 1:       +49.0°C  (high = +100.0°C, crit = +100.0°C)
```

Láthatóan nem igazán sikerült nálam a detektálás, a legtöbb értéknél ( temp1, ..., temp6 ) igazából nem egyértelmű, hogy mihez is kapcsolódik a szenzor.