---
layout: post
title: 'cp helyett rsync'
permalink: /2017/03/09/cp_helyett_rsync
post_id: 12322619
categories: 
- cp
- rsync
---

A cp (copy) parancs az egyik legalapvetőbb utasítás, de van néhány hátránya. Leginkább engem az zavar, hogy nem kapok arról visszajelzést, hogy hol is tart a másolás. Elég sokan azt 
[javasolják](http://stackoverflow.com/a/6339326/21348), hogy használjunk inkább 
[rsync](https://rsync.samba.org/)-et. Korábban erről a parancsról már 
[írtam](http://commandline.blog.hu/2010/06/29/rsync), archiváláshoz használom.

Ha cp helyett a következő paraméterezését szoktam használni:

```
rsync -ah --progress
```

Bátrabbak akár a alias-t is beállíthatnak, hogy cp helyett ez fusson, ezzel kapcsolatban azért vannak fenntartásaim.