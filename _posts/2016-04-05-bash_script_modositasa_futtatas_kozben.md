---
layout: post
title: 'bash script módosítása futtatás közben'
permalink: https://commandline.blog.hu/2016/04/05/bash_script_modositasa_futtatas_kozben
post_id: 8554258
categories: 
- bash
---

Manapság elég lassú bash scripteket futtatok és többször előfordult, hogy már a futás közben láttam, hogy mit kell majd a scriptben módosítani. Jó ötletnek tűnt a futás közben módosítani a scriptet, hogy a script befejezésekor rögtön el tudjam indítani az új változatot. Teljesen furcsa és érthetetlen hibajelzéseket kaptam ezért utánanéztem, és sajnos úgy tűnik, hogy bash nem olvassa be az egész scriptet a végrehajtás elején, hanem mindig csak az a kis részét amivel foglalkozik. Itt most ne óriási scriptekre gondoljunk, néhány kilobájtos scripteknél is tapasztaltam ezt, amelyek kényelmesen elférnének a memóriában.

Úgy tűnik nemcsak én gondoltam azt, hogy bátran módosíthatjuk a scripteket, ennél a 
[stackoverflows kérdésnél](http://stackoverflow.com/q/3398258/21348) is látszik, hogy a logikusnak tűnő elfogadott válasz -12 ( már -13 ) szavazatnál jár.