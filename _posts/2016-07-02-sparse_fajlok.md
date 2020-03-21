---
layout: post
title: 'sparse fájlok'
permalink: https://commandline.blog.hu/2016/07/02/sparse_fajlok
post_id: 8853758
categories: 
- dd
- sparse
---

Ha szükségem volt egy nagy tesztfájlra, többnyire a következő módszerrel készítettem a fájlt:

```
$ time dd if=/dev/zero bs=$((1024*1024)) count=1024 of=large.dat
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB) copied, 12.3933 s, 86.6 MB/s
real    0m12.394s
user    0m0.005s
sys     0m0.480s
```

Az 1GB-os fájl elkészítése kb. 12 másodperc volt.

Listázzuk ki a fájlt, az egyszerűség kedvéért 1024 bájtos blokkméretben megnézve az elfoglalt blokkok számát:

```
$ ls -lsk large.dat 
1048580 -rw-r--r-- 1 user live 1073741824 Jun 11 17:18 large.dat
```

Az 1048580 db. blokk reálisnak tűnik, 1024-gyel szorozva kb. 1GB-ot kapunk, a különbség (4096 byte) elhanyagolható.

Mivel a fájlt csupa 0-ból áll, elvileg van egy másik mód is az 1GB-os fájl létrehozására:

```
$ time dd if=/dev/zero bs=1 count=1 of=large2.dat seek=$((1024*1024*1024-1))
1+0 records in
1+0 records out
1 byte (1 B) copied, 6.7613e-05 s, 14.8 kB/s
real    0m0.001s
user    0m0.000s
sys     0m0.000s
```

Ebben a példában dd-vel egyetlen bájtot iratok csak a fájlba, azt viszont seek segítségével pont ugyanoda írom ahol az előző példában a fájl vége volt. A parancs döbbenetesen gyorsan lefut, elég nyilvánvaló, hogy ennyi idő nem elég 1GB-nyi 0 lemezre írására.

Listázzuk ki a két fájlt:

```
$ ls -lsk large*
      4 -rw-r--r-- 1 user live 1073741824 Jun 11 17:19 large2.dat
1048580 -rw-r--r-- 1 user live 1073741824 Jun 11 17:18 large.dat
```

A fájlméret bájtra megegyezik, viszont az új fájl összesen csak 4 blokkot foglal az 1 GB helyett mivel 
[sparse (ritka?) fájl](https://en.wikipedia.org/wiki/Sparse_file) jön létre, a rendszer nem tárolja feleslegesen a sok-sok 0 bájtot.

Nem minden fájlrendszer támogatja ezt, én ext3-mal teszteltem.

Az előnyei mellett nyilvánvaló veszélyei is vannak az ilyen fájloknak, például az ilyen fájlokat módosítva könnyen elfogyhat a lemezen a szabad hely akkor is, ha a látszólagos fájlméret nem nő.

 