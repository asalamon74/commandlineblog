---
layout: post
title: 'patch készítése'
permalink: /2012/02/27/patch_keszitese
post_id: 4208434
categories: 
- patch
- pentax
- diff
- digitális_fénykép
---

A már említett 
[diff](http://commandline.blog.hu/2011/09/04/diff_1) parancs segítségével egy programon elvégzett módosításainkból 
[patcheket](http://hu.wikipedia.org/wiki/Patch)készíthetünk. A következő példa szándékosan leegyszerűsített, de egy valódi programhoz készített patchet mutat be. 
A Pentax K-x gép által készített DNG fájl 4352x2868 pixel, de a kép jobb szélen több oszlopnyi fekete pixel található. Ha 
[exiftool](http://commandline.blog.hu/2010/05/14/exiftool) segítségével belenézünk a DNG fájlba, azt is látjuk, hogy default cropnak 4288x2848-as méret van beállítva a 10,10 koordinátájú pixeltől kezdve. A raw konverterek eléggé eltérően kezelik ezt a furcsaságot, a 
[már korábban említett](http://commandline.blog.hu/2010/05/11/raw_konvertalasa_jpg_re) 
[ufraw](http://ufraw.sourceforge.net/) program egyszerűen levágja a kép jobb szélét és 4309x2868 méretű jpeg fájlokat gyárt. Ez elég furcsa méret, ehelyett én jobban szeretem, ha pont 3:2 arányú az oldal, ezért 4272x2848-as méretet szeretnék. Ehhez alul és felül 10-10 pixelt,  balra 18, jobbra 62 pixelt szeretnék levágni ( a jobb oldali 44 pixel fekete miatt nem szimmetrikus a vágás). 
Ha belenézünk ufraw forrásába, akkor dcraw.cc fájlban találjuk a következő részt, ami meghatározza a vágás méretét: 
```
  if (!strcmp(model,"K-r") || !strcmp(model,"K-x"))
     {                   width  = 4309; filters = 0x16161616; }
``` 
Ezt kell módosítani erre: 
```
  if (!strcmp(model,"K-r") || !strcmp(model,"K-x"))
     { left_margin = 18; height = 2848; top_margin = 10; width  = 4272; filters = 0x16161616; }
```
  
Egy ilyen egyszerű esetben még csak-csak el lehet magyarázni, hogy mit kell átírni, de ha több fájlt módosítunk több helyen, akkor ez követhetetlen. Ehelyett érdemes egy alkönyvtárban ( a példában: ufraw-0.18) a program eredeti változatát, egy másik alkönyvtárban ( a példában: ufraw-0.18_modified) a program módosított változatát eltárolni, és patchet készíteni: 
```
diff -uNr ufraw-0.18 ufraw-0.18_modified > ufraw_kx.patch
``` 
Figyeljünk arra oda, hogy a két alkönyvtár a módosításunkat leszámítva egyforma legyen! Ne felejtsünk ott például tesztfájlokat! A parancs hatására a következő fájlt kapjuk: 
```
diff -uNr ufraw-0.18/dcraw.cc ufraw-0.18_modified/dcraw.cc
 --- ufraw-0.18/dcraw.cc 2011-02-20 08:56:15.000000000 +0100
 +++ ufraw-0.18_modified/dcraw.cc        2012-02-26 10:39:23.452480315 +0100
 @@ -7104,7 +7104,7 @@
    if (height == 3136 && width == 4864)  /* Pentax K20D and Samsung GX20 */
      { height  = 3124;   width  = 4688; filters = 0x16161616; }
    if (!strcmp(model,"K-r") || !strcmp(model,"K-x"))
 -    {                  width  = 4309; filters = 0x16161616; }
 +    { left_margin = 18; height = 2848; top_margin = 10; width  = 4272; filters = 0x16161616; }
    if (!strcmp(model,"K-5"))
      { left_margin = 10; width  = 4950; filters = 0x16161616; }
    if (!strcmp(model,"K-7"))
```
 Ez a fájl írja le a módosításainkat olyan formában, amit a patch parancs megért. Ha elküldjük a patchet valakinek akinél az eredeti ufraw-0.18 alkönyvtár van, a következő módon tudja frissíteni a programot: 
```
$ patch -p0 < ufraw_kx.patch 
 patching file ufraw-0.18/dcraw.cc
``` 
A módszer akkor is hasznos ha saját magunknak akarjuk eltárolni a módosításokat, de különösen akkor hasznos, ha egy nyílt forráskódú program fejlesztésében akarunk segíteni.