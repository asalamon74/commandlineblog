---
layout: post
title: 'Véletlenszám'
permalink: https://commandline.blog.hu/2013/04/14/veletlenszam
post_id: 5220652
categories: 
- random
- véletlenszám
- urandom
---

Ha egy véletlenszámra van szükségünk, akkor legegyszerűbb a $RANDOM környezeti változó használata, ami 0 és 32767 között ad egy véletleszámot:

```
$ echo $RANDOM
7161
$ echo $RANDOM
6322
```

Szinte minden weboldalon ahol írnak róla a kockadobást hozzák fel példának, így én is ezt teszem:

```
$ echo $(($RANDOM % 6 + 1))
5
$ echo $(($RANDOM % 6 + 1))
4
```

Ha nem egyszerűen egyetlen véletlenszámra van szükségünk, hanem pl. egy 1024 bájtból álló véletlen sorozatra, akkor /dev/urandom-ból érdemes dd-vel olvasnunk:

```
$ if=/dev/urandom of=urandom.dat bs=1024 count=1
1+0 records in
1+0 records out
1024 bytes (1.0 kB) copied, 0.000456885 s, 2.2 MB/s
```

 Nyilván felmerül a kérdés, miért /dev/urandom-ot használunk, miért nem /dev/random-ot. Próbáljuk meg azt:

```
$ dd if=/dev/random of=random.dat bs=1024 count=1
0+1 records in
0+1 records out
16 bytes (16 B) copied, 8.0245e-05 s, 199 kB/s
```

Meglepő, de hiába kértem 1 db. 1024 bájtos adatcsomagot, csak 16 bájtot kaptam. Kérjünk inkább 1024 db. 1 bájtos csomagot:

```
$ dd if=/dev/random of=random.dat bs=1 count=1024
1024+0 records in
1024+0 records out
1024 bytes (1.0 kB) copied, 99.2821 s, 0.0 kB/s
```

Ezzel már sikerült 1024 bájt kiolvasása, de több mint 1 percet kellett az eredményre várni. Ha 1GB véletlen adatra lenne szükségünk, akkor reménytelen lenne kivárni ameddig összegyűlik az adat.

A /dev/random és /dev/urandom közti különbségről 
[több](http://en.wikipedia.org/wiki//dev/random) 
[helyen](http://stackoverflow.com/q/5635277/21348) is írnak, a lényeg az, hogy /dev/random "igazibb" véletlenszámokat ad az egyes hardverelemek entrópiáinak felhasználásával, de cserébe hamar elfogynak a rendelkezésre álló bájtok, ilyenkor vár addig ameddig újra össze nem gyűlik megfelelő mennyiségű adat. Ezzel szemben /dev/urandom folyamatosan képes véletlenszámokat adni, cserébe az alacsonyabb minőségért. Az esetek többségében a /dev/urandom is megelelő számunkra, hacsak nem valami komoly kriptográfiai célra kellenek az adatok.