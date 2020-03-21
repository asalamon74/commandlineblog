---
layout: post
title: 'SysRq REISUB'
permalink: https://commandline.blog.hu/2012/02/24/sysrq_reisub
post_id: 4130669
categories: 
- boot
- sysrq
---

Bevallom, hosszú évek alatt sosem gondolkodtam el azon, hogy mi az a sys rq gomb a billentyűzetemen, de egy érdekes 
[commandlinefu bejegyzés](http://www.commandlinefu.com/commands/view/1081/reboot-machine-when-everything-is-hanging) hatására 
[utánanéztem](http://en.wikipedia.org/wiki/Magic_SysRq_key). A gomb segítségével alacsony szintű utasításokat adhatunk a Linux kernelnek, így egy lefagyott gépet éleszthetünk újra, vagy legalább fájdalommentesen újraindíthatunk.

A sok lehetőség közül először az m betűvel elérhető ( memóriainformációt /var/log/syslog ill. /var/log/messages fájlba író ) parancsot próbáltam ki. A leírásnak megfelelően sok lehetőséget kipróbálva az én gépemen a következő módon használható a módszer:

* alt gr lenyomása


* fn lenyomása


* sys rq/delete lenyomása


* fn felengedése


* sys rq/delete felengedése


* m lenyomása


* m felengedése


* alt gr felengedése

A memóriainformációkért persze nem éri meg ennyit szenvedni, a SysRq leginkább hasznos funkciója a biztonságos bootolás, amit a REISUB parancsokkal érhetünk el:

* r: billentyűzet vezérlés visszavétele X-től


* e: SIGTERM küldése az összes processnek


* i: SIGKILL küldése az összes processnek


* s: adatok kiírása a diszkekre


* u: read-only módban újramountolása a diszkeknek


* b: újraindítás

Az egyes betűk után érdemes pár másodpercet várni, hogy lefuthassanak a parancsok.

Mivel a gépen éppen rendesen működik, azt nem teszteltem ki, hogy tényleg újraindít-e egy lefagyott gépet. A rendesen működő gépet valóban jól újraindította.