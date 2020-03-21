---
layout: post
title: 'encfs --reverse'
permalink: /2016/12/03/encfs_--reverse
post_id: 12010714
categories: 
- backup
- titkosítás
- encfs
---

Általában ha egy alkönyvtárat titkosítunk (pl. 
[encfs](http://commandline.blog.hu/2010/01/19/encfs)sel) akkor titkosítva tároljuk az adatokat a merevlemezen és csak jelszóval férhetünk hozzá a titkosítatlan adatokhoz. Lehetőségünk van ennek a fordítottjára is.

Akiben felmerül, hogy mi értelme van ennek: Van egy alkönyvtáram amit lokálisan nincsen titkosítva (annyira nem tikos) de azért a felhőbe nem szeretném titkosítatlanul feltölteni.

Ha van egy titkosítatlan alkönyvtárunk (/tmp/dir1) akkor a következő paranccsal titkosíthatjuk ezt:

```
encfs --reverse /tmp/dir1 /tmp/dir2
```

Néhány kérdés után (a jelszót is meg kell adnunk kétszer) létrejön a /tmp/dir2 alkönyvtár, ami a /tmp/dir1 titkosított változata. Már a fájlnevek is titkosítva vannak benne, így nem kell attól sem tartanunk, hogy a fájlnevek sokat elárulnak a tartalomról. Valójában ez persze csak egy virtuális fájlrendszer, vagyis nem fog órákig futni a titkosítás és nem is foglal el helyet a merevlemezen.

Nagyon fontos, hogyha vissza szeretnénk állítani a titkosított állapotból az eredetit, akkor nem elég a /tmp/dir2 alkönyvtár tartalma. Az előző parancs létrehoz még egy rejtett fájlt (/tmp/dir1/.encfs6.xml) amire szintén szükségünk lesz (és persze a jelszóra is):

```
ENCFS6_CONFIG=/tmp/dir1/.encfs6.xml encfs /tmp/dir2 /tmp/dir3
```

Ezután /tmp/dir3 az eredeti titkosítatlan verziót mutatja.

A backup programtól függően az is lehet, hogy encfs --reverse parancsot inkább rootként --public kapcsolóval együtt érdemes futtatnunk.

 

 