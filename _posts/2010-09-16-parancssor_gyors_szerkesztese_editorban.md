---
layout: post
title: 'Parancssor gyors szerkesztése editorban'
permalink: https://commandline.blog.hu/2010/09/16/parancssor_gyors_szerkesztese_editorban
post_id: 2297534
categories: 
- editor
- vi
- bash
- emacs
---

Ha éppen valami igen bonyolult parancssort editálunk, akkor könnyen lehet, hogy a shell beépített 
[egyszerű editora](http://commandline.blog.hu/2010/04/23/bash_soreditalas) helyett szívesebben használnánk kedvenc editorunkat (emacs, vi, ...). Persze készíthetünk az éppen editált parancssor helyett egy 1 soros scriptet, amit külön editorban editálunk, de ha ez az editálás kellős-közepén jut eszünkbe (többnyire akkor szokott), akkor ez nem túl kényelmes. 
Ehelyett sokkal egyszerűbb, ha az editálás közben lenyomjuk a következő billentyűkombinációt: 
```
ctrl-x ctrl-e
``` 
Ennek hatására megnyílik kedvenc szövegszerkesztőnk (feltéve, hogy EDITOR környezeti változó rendesen be van állítva) az éppen editált parancssorral. Ha befejeztük az editálást, és becsukjuk az editort, akkor nyomban le is fut a parancs.