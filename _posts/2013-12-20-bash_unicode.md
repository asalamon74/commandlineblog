---
layout: post
title: 'bash + unicode'
permalink: https://commandline.blog.hu/2013/12/20/bash_unicode
post_id: 5693212
categories:  []
---

Nem tudom ki emlékszik rá, de a 
[DOS](http://hu.wikipedia.org/wiki/DOS)-os időkben elég macerás volt ékezetes karaktereket gépelni, ehelyett Alt-kódokkal lehetett a speciális magyar karaktereket elérni. Még mindig emlékszem rá, hogy Alt+160 volt az á, Alt+130 az é ( 
[itt](http://tools.oratory.com/altcodes.html) a többi kód ). Egy idő után elég gyorsan ment így a gépelés...

Szerencsére jó ideje nem kell így gépelnem, de nemrég egy speciális Unicode karaktert akartam begépelni bash parancssorban, és megint jól jött volna ez a módszer. Utánanéztem, és azt 
[találtam](http://stackoverflow.com/a/5955592/21348), hogy CTRL-SHIFT-U lenyomása majd felengedése után a prompt egy aláhúzott 
u betűre vált ahol a hexadecimális Unicode kód beírásával írhatjuk be a speciális karaktereket.

Kipróbáltam, és a blog.hu editorában Firefox alatt is működik: şğç