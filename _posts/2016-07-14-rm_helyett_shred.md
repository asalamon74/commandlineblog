---
layout: post
title: 'rm helyett shred'
permalink: https://commandline.blog.hu/2016/07/14/rm_helyett_shred
post_id: 8871668
categories: 
- rm
- shred
---

Korábban már használtam shredet a 
[merevlemez teljes tartalmának törléséhez](http://commandline.blog.hu/2011/03/06/merevlemez_torlese), de ezt használhatjuk fájltörléshez is.

/dev/sdb6 partíción teszteltem:

```
$ echo 'EZNINCSAPARTICION' > test1.txt
 $ strings /dev/sdb6 | grep -i EZNINCS
EZNINCSAPARTICION
$ rm -f test1.txt 
$ strings /dev/sdb6 | grep -i EZNINCS
EZNINCSAPARTICION
```

Látszik, hogy a fájl törlése után is megmarad a partíción a fájl tartalma.

```
$ echo 'EZTENYLEGNINCSAPARTICION' > test2.txt
$ strings /dev/sdb6 | grep -i EZTENYLEG
EZTENYLEGNINCSAPARTICION
$ shred --remove test2.txt
 $ sudo strings /dev/sdb6 | grep -i EZTENYLEG
 $
```

Ha rm helyett shred-et használunk, akkor törlés után nincs nyoma a fájl eredeti tartalmának.