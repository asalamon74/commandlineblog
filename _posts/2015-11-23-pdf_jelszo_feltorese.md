---
layout: post
title: 'pdf jelszó feltörése'
permalink: /2015/11/23/pdf_jelszo_feltorese
post_id: 8097800
categories: 
- jelszó
- pdf
- pdfcrack
---

Nemrég 
[írtam](/2015/11/20/pdf_jelszovedelem) arról, hogyan adhatunk jelszóvédelmet egy pdf fájlhoz, adódik a kérdés, hogyan törhetjük ezt fel. Az előző példában használt 1234 jelszót elég gyorsan (laptopomon 5 perc) feltörhetjuk 
[pdfcrack](http://pdfcrack.sourceforge.net/) segítségével:

```
$ pdfcrack titok_jelszo.pdf
PDF version 1.5
Security Handler: Standard
V: 2
R: 3
P: -3904
Length: 128
Encrypted Metadata: True
FileID: c2188884ae81630733b6fa0ad14ef5f2
U: d512a0db3b14300dcf3a97c585ca164e00000000000000000000000000000000
O: c48f001fdd79a030d718df6dbbdaad81d1f6fedec4a7b5cd980d64139edfcb7e
Average Speed: 47776.9 w/s. Current Word: '3I9c'
Average Speed: 47711.2 w/s. Current Word: 'LX9g'
Average Speed: 47709.5 w/s. Current Word: 'Vbal'
Average Speed: 47700.9 w/s. Current Word: 'knap'
Average Speed: 47222.0 w/s. Current Word: 'e47s'
Average Speed: 46564.5 w/s. Current Word: '2k2w'
Average Speed: 46664.3 w/s. Current Word: '27WA'
Average Speed: 47224.7 w/s. Current Word: 'OPUE'
Average Speed: 47014.5 w/s. Current Word: 'MrRI'
Average Speed: 47014.7 w/s. Current Word: 'N3NM'
Average Speed: 46364.2 w/s. Current Word: '0hHQ'
Average Speed: 46843.7 w/s. Current Word: 'S0CU'
Average Speed: 46919.4 w/s. Current Word: 'b8yY'
Average Speed: 46733.1 w/s. Current Word: 'mhu2'
found user-password: '1234'
```

5 perc nem hosszú idő, de azért a kb. 50000 jelszó/másodperc azt is mutatja, hogy egy kicsit hosszabb jelszót már nehezen törne fel a program. Kivéve, ha van valami plusz információnk. Igen gyakran védenek jelszóval pdf fájlt úgy, hogy csak számjegyeket használnak a jelszóban. Megadva ezt az információt pdfcracknek már gyorsabb a törés:

```
$ pdfcrack titok_jelszo_6.pdf -c 0123456789
PDF version 1.5
Security Handler: Standard
V: 2
R: 3
P: -3904
Length: 128
Encrypted Metadata: True
FileID: b36c321f38d07288f29b3a893a8133db
U: 90844e112863b7c974f5afaaf857107b00000000000000000000000000000000
O: c431fab9dc5ef7b59c244b61b745f71ac5bb427b1b9102da468e77127f1e69d6
found user-password: '123456'
```

16 másodperc elég az 123456 jelszó megtalálásához.

Megadhatjuk a programnak ezen kívül a jelszó minimális illetve maximális hosszát, képest szólista alapján (password, passw0rd, qwertz, abc123,...) dolgozni. Ha nagyon lassú a törés, akkor a részeredményeket elmenthetjük és később folytathatjuk a munkát. A program egyetlen hiányossága talán az, hogy nem támogatja a többmagos processzorokat.

Ha valaki látja a jelszavát ebben a bejegyzésben, sűrgősen változtassa meg!