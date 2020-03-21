---
layout: post
title: 'Fájlméretek összeadása'
permalink: /2011/07/30/fajlmeretek
post_id: 3107411
categories: 
- awk
---

Egy
[korábbi bejegyzésben](/2010/07/31/du_1) írtam a du parancsról, aminek segítségével az alkönyvtárak által elfoglalt lemezterületet tudjuk ellenőrizni. Az ott leírt módszer nem használható, ha nem az egész alkönyvtárra vagyunk kíváncsiak, csak az ott található fájlok egy részére. 
Egy alkönyvtáramban vegyesen vannak tömörített és tömörítetlen log fájlok. A tömörítetlen logfájlok összméretére voltam kíváncsi: 
```
find . -name "*.log" -printf "%s\n"|awk '{sum+=$0}END{print sum}'
``` 
Némi magyarázat: 
* A 
[find](/2010/11/14/find_2) paranccsal kerestem meg az engem érdeklő fájlokat. Itt elég egyszerű a szabály.
     
* A 
```
-printf "%s\n"
```
 hatására find nem a talált fájlok neveit írja ki, hanem a fájlméreteket szépen külön sorban.
* Az így kapott számokat 
[awk](http://en.wikipedia.org/wiki/Awk) segítségével adom össze.
* A legvégén (END) pedig kiiratom az összeget. 
 