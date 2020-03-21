---
layout: post
title: 'pushd popd'
permalink: /2010/01/16/pushd_popd
post_id: 1635328
categories: 
- cd
- verem
- pushd
- popd
- alkönyvtár
---

Ha egyszerre több alkönyvtárban is dolgozni szeretnénk, és ida-oda akarunk váltani, akkor a 
```
cd
```
 parancs helyett érdemesebb a 
```
pushd, popd
```
 párost használni. Míg 
```
cd
```
 alkönyvtárat vált, és nem őriz meg információt arról, korábban melyik alkönyvtárban voltunk, 
```
pushd
```
 és 
```
popd
```
 egy egy alkönyvtár vermet tart nyilván. 
```
pushd
```
 alkönyvtárat vált és az új alkönyvtárat a verem tetejére teszi, 
```
popd
```
 a verem tetején található alkönyvtárra vált, és törli a verem legfelső elemét. Mindkét parancs kiírja a verem tartalmát is ( ezt a 
```
dirs
```
 paranccsal is elérhetjük ).

```
[/tmp]# pushd /media/cdrom

/media/cdrom /tmp

[/media/cdrom]# pushd /mnt

/mnt /media/cdrom /tmp

[/mnt]# popd

/media/cdrom /tmp

[/media/cdrom]# popd

/tmp

[/tmp]# popd

bash: popd: directory stack empty

[/tmp]#
```
 



Ha két alkönyvtár között szeretnénk váltani, akkor a 
```
pushd
```
-t paraméterek nélkül használjuk:

```
[/tmp]# pushd /media/cdrom

/media/cdrom /tmp

[/media/cdrom]# pushd

/tmp /media/cdrom

[/tmp]# pushd

/media/cdrom /tmp

[/media/cdrom]#
```