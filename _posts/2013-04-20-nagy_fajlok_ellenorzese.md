---
layout: post
title: 'Nagy fájlok ellenőrzése'
permalink: https://commandline.blog.hu/2013/04/20/nagy_fajlok_ellenorzese
post_id: 5234503
categories: 
- kriptográfia
- hash
- md5sum
- cksum
- sha256sum
- sha512sum
---

Ha egy nagy fájlt szeretnénk az internetről letölteni akkor többnyire a nagyméretű fájl ( továbbiakban nagyfile.iso ) mellett találunk egy nagyfile.iso.md5 fájlt is, ami mindössze néhány bájtos, és segítségével a letöltött nagyméretű fájl integritását ellenőrízhetjük.

Egy fájl integritásának ellenőrzésekor legegyszerűbb egy 
[CRC](http://en.wikipedia.org/wiki/Cyclic_redundancy_check) ellenőrzőösszeg számítása, ugyanakkor a módszer igen nagy hátránya, hogy csak a véletlenül előforduló hibák ellen véd. Vagyis azt ki tudjuk ezzel szűrni, ha a letöltött 4GB-os fájl néhány bájtja megsérül a letöltés során, de azt nem, ha valaki szándékosan módosítja úgy a fájlt, ha a CRC összeg ne változzon. Ha ennek ellenére valaki ezt szeretné használni, akkor a 
[cksum](http://en.wikipedia.org/wiki/Cksum) paranccsal teheti meg.

Ha a szándékos károkozást is deketálni szeretnénk, akkor 
[kriptográfiai hash függvényt](http://hu.wikipedia.org/wiki/Kriptogr%C3%A1fiai_hash_f%C3%BCggv%C3%A9ny) kell használnunk. A legelterjedtebbnek nekem az 
[MD5](http://en.wikipedia.org/wiki/MD5) tűnik.

MD5 fájlt így gyárthatunk:

```
$ md5sum nagyfile.iso > nagyfile.iso.md5
$ cat nagyfile.iso.md5 
45371276b1406fb29640fa564d818e24  nagyfile.iso
```

Az ellenőrzés pedig így megy:

```
$ md5sum -c nagyfile.iso.md5
nagyfile.iso: OK
```

Érdemes azért tudni, hogy a legelterjedtebb MD5 függvényt már nem tekintik biztonságosnak, sőt az ennél jobbnak számító 
[SHA1](http://en.wikipedia.org/wiki/SHA-1) ellen is létezik már elméleti törés. Használjunk inkább 
[sha256](http://linux.die.net/man/1/sha256sum) vagy 
[sha512](http://linux.die.net/man/1/sha512sum) függvényeket.

Halkan merem csak írni, de szerintem valójában csak a biztonság illúzióját nyújtják ezek a módszerek, legalábbis a letöltők 99%-a számára nem nyújtanak többet mint egy sima CRC ellenőrzés. Az egész módszer azt feltételezi, hogy az ellenőrzéshez használt fájl ( fenti példában nagyfile.iso.md5 ) már a birtokunkban van, és teljesen biztosak lehetünk a tartalmában. Ha egyszerre töltjük le nagyfile.iso nagyfile.iso.md5 fájlokat ugyanarról a szerverről, akkor ez nem igaz, ha valaki módosította nagyfile.iso-t, akkor módosíthatta nagyfile.iso.md5-öt is. Az md5 fájl ellenőrzését általában úgy oldják meg, hogy egy nagyfile.iso.md5.gpg fájlt is felmásolnak, aminek segítségével ellenőrizhetjük a nagyfile.iso.md5 fájlt. Feltéve, hogy kezünkben van az aláíró nyilvános kulcsa, amit nyilván megint nem szerencsés ugyanekkor ugyanarról a szerverről letölteni. Vagyis bár elvileg tényleg alaposan ellenőrizhetünk mindent, a valóságban a legtöbb ember letölt két fájlt, futtat egy md5sum -c parancsot és megnyugszik.