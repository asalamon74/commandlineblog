---
layout: post
title: 'Kiterjesztés levágása'
permalink: /2016/04/11/kiterjesztes_levagasa
post_id: 8575892
categories: 
- bash
- basename
---

Valójában csak azért írtam pár napja a 
[basename](/2016/04/08/basename)-ról, hogy egy hiányosságára felhívjam a figyelmet. Ha egy scriptünk jpg fájlokkal dolgozik, akkor könnyen levághatjuk a kiterjesztést:

```
$ basename alma.jpg .jpg
 alma
```

Ha viszont egy olyan scriptet írunk ami többféle formátummal is dolgozhat, akkor a basename-et nem tudjuk használni, mert nincs olyan paraméterezése (legalábbis nem tudok róla) ami az összes kiterjesztést levágja.

Ha csak kétféle kiterjesztést kell kezelni, akkor néha 2 basename-mel oldom ezt meg, de erre nem vagyok büszke. A következő módon a jpg és png kiterjesztést is le lehet vágni:

```
$ basename $(basename alma.jpg .jpg) .png
alma
$ basename $(basename alma.png .jpg) .png
alma
```

Ha univerzálisan akarjuk a kiterjesztést levágni, akkor a bash beépített lehetőségeit használhatjuk:

```
$ s=input.jpg
$ echo ${s%.*}
input
```

Ha nemcsak a kiterjesztést, hanem az alkönyvtárat is le akarjuk vágni (hasonlóan basename-hez) akkor kicsit még bonyolultabb a használat:

```
$ s=/tmp/input.jpg
 $ echo ${s%.*}
 /tmp/input
 $ s2=${s##*/}
$ echo ${s2%.*}
input
```

 