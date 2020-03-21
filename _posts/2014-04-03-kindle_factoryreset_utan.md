---
layout: post
title: 'Kindle factoryreset után'
permalink: /2014/04/03/kindle_factoryreset_utan
post_id: 5890678
categories: 
- kindle
---

Kíváncsi voltam, vajon egy Kindle ( Keyboard 3G ) törlése ( factory reset ) után mennyi adat marad az eszközön. Vagyis valójában inkább arra, hogy eladás előtt elég-e a factory reset. Először 
[rákérdeztem](http://ebooks.stackexchange.com/q/982/91), de mivel túl konkrét választ nem kaptam végeztem egy kis 
[tesztet](http://ebooks.stackexchange.com/a/1190/91).

A következő nagyon egyszerű script factory reset után is szépen kilistázza a Kindle korábbi könyveit:

```
$ dd if=/dev/sdc1 of=afterfactoryreset.dat bs=1M
 $ strings afterfactoryreset.dat | grep -i '^mnt/us/documents' | rev | cut -d "." -f2- | rev | sort | uniq
mnt/us/documents/A Clash of Kings A Song of Ice a-asin_B000FC1HBY-type_EBOK-v_0
...
mnt/us/documents/Zendegi-asin_B003NE5TVU-type_EBOK-v_0
```

 