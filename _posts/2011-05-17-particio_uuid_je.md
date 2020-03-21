---
layout: post
title: 'Partíció UUID-je'
permalink: /2011/05/17/particio_uuid_je
post_id: 2909152
categories: 
- e2fsprogs
- blkid
---

Egy partíció egyedi azonosítójára (
[UUID](http://en.wikipedia.org/wiki/Universally_unique_identifier)) vagyunk kíváncsiak, a 
```
blkid
```
 parancs segítségével ( 
[e2fsprogs](http://e2fsprogs.sourceforge.net/) csomag része ) tudhatjuk meg: 
```
# blkid /dev/sda10
 /dev/sda10: UUID="186567b7-48f9-45a8-b650-7362ee6ee3b3" TYPE="ext4"
```