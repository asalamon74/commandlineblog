---
layout: post
title: 'bash: alapértelmezett érték'
permalink: /2015/10/12/bash_alapertelmezett_ertek
post_id: 7956946
categories: 
- bash
- default_value
---

Ha írunk egy bash scriptet elég gyakori, hogy paramétereket is átadhatunk a scriptünknek, melyekre $1 $2 ... néven hivatkozhatunk. Szintén elég gyakori, hogy a paraméterek egy része opcionális. A következő igen egyszerű példában három paramétert fogad el a scipt, melyek alapértelmezett értékei rendre 100, 200, 300:

```
#!/bin/bash
 echo ${1-100} ${2-200} ${3-300}
```

A script tesztelése:

```
$ teszt.sh a b c
a b c
$ teszt.sh a b
a b 300
$ teszt.sh a
a 200 300
$ teszt.sh
100 200 300
```

Bár nem igazán szoktam a nyelvek szintaxisát kritizálni, azért azt meg kell jegyeznem, hogy nem kicsit félrevezető a ${1-100} forma. Ha az 5. paraméterünk alapértelmezett értéke 1, akkor ${5-1}-et kell írni, ami még véletlenül sem ${4}.