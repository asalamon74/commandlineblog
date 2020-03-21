---
layout: post
title: 'Bash parancssori kiegészítés'
permalink: https://commandline.blog.hu/2012/01/20/bash_parancssori_kiegeszites
post_id: 3592343
categories: 
- bash
- bash_completion
---

A Linux operációs rendszer alatt leggyakrabban használt shell program a 
[bash](http://www.gnu.org/software/bash/bash.html), az összetett program tudásának azonban többnyire csak töredékét használjuk.

Valószínűleg mindannyian használjuk a parancsok és filenevek kiegészítésének lehetőségét. Elég a parancs első betűit beírnunk és a 
```
TAB
```
 billentyűt leütnünk, és a shell megpróbálja kiegészíteni a parancsot. Ha csak egy parancs kezdődik a beírt betűkkel, akkor automatikusan kiegészítődik, ha több lehetséges kiegészítés is van, akkor a 
```
TAB
```
 újbóli lenyomása után megkapjuk a lehetséges parancsok listáját.

Ha a parancsot már beírtuk, akkor a 
```
TAB
```
 a filenevek kiegészítését segíti. Mivel parancssorban gyakran adunk filenevet paraméternek, ez a kiegészítési mód nagyon hasznos.

Vannak esetek, amikor nem szerencsés, hogy az összes file nevét figyelembe veszi a shell a kiegészítéskor. Ha az 
```
acroread
```
 vagy 
```
xpdf
```
 parancsokkal egy pdf dokumentumot szeretnénk megnézni, akkor sokkal jobb lenne, ha a kiegészítés csak a pdf kiterjesztéssel rendelkező file-okat venné figyelembe.

Szerencsére elég régóta (bash 2.04 béta verziójától kezdve) lehetőségünk van a kiegészítés átprogramozására a beépített 
```
complete
```
 utasítás segítségével.

```
complete -f -X '!*.pdf' acroread
```

Az utasítás hatására az 
```
acroread
```
 parancs után csak a pdf kiterjesztéssel rendelkező file-okat veszi figyelembe a shell. A 
```
-f
```
 opció jelöli, hogy a kiegészítésben a fileneveket kell figyelembe venni, a 
```
-X
```
 opció után azt kell megadnunk (egy mintával), melyeket 
nem akarunk a kiegészítés során használni. Ezért kellett a példában a negálást jelző felkiáltójelet használnunk, hiszen mi csak a *.pdf mintára illeszkedő fileneveket szeretnénk használni. Ha több kiterjesztést is szeretnénk engedélyezni, vagy több programhoz is ugyanazokat a kiterjesztéseket használni, akkor ezt is könnyen megtehetjük:

```
complete -f -X '!*.@(dvi|DVI)' dvips dviselect dvitype
```

Az utasítás hatására a 
```
dvips
```
, 
```
dviselect
```
 és 
```
dvitype
```
 parancsok után csak a .dvi vagy .DVI kiterjesztéssel rendelkező file-okat veszi figyelembe a bash. A példában a kiegészítés során a filenevek listájából választhattunk. Vannak olyan esetek is, amikor nem file-okra van szükségünk, hanem például a felhasználók nevére. Ilyenkor a 
```
-f
```
 helyett más opciót kell használnunk. A következő táblázat a legfontosabb opciókat tartalmazza, a teljes listát a 
```
man bash
```
 segítségével ismerhetjük meg.

OpcióKiegészítés során figyelembe vett dolgok

-d

Alkönyvtárak

-f

Filenevek

-g

Csoportok

-u

Felhasználók nevei

-v

Shell változók

-W

Az opció után felsorolt szavak

 

Ha a 
```
finger
```
, 
```
su
```
, 
```
usermod
```
, 
```
userdel
```
, 
```
passwd
```
 parancsok után csak a felhasználók nevét szeretnénk használni, könnyen megtehetjük a következő paranccsal:

```
complete -u finger su usermod userdel passwd
```

Bár a fentiek alapján mindenki saját maga tudja programozni az automatikus kiegészítést, egyszerűbb letölteni egy olyan programot, ami megteszi ezt helyettünk. A 
[bash-completion](http://www.caliban.org/bash/) csomag több mint száz parancs (pl. 
```
man, cvs, rpm, find, apt-get, ...
```
) automatikus kiegészítését programozza át. A fenti egyszerű példákat mind a csomagból vettem, a csomag természetesen sokkal bonyolultabb példákat is tartalmaz, olyanokat például, ahol a parancs korábbi paraméterétől is függ a kiegészítés.

Ha szeretnénk megnézni, miként működik a csomag, vagy szeretnénk esetleg kiegészíteni, akkor a 
```
/etc/bash_completion
```
 file-t illetve a /etc/bash_completion.d alkönyvtárat kell megnéznünk.