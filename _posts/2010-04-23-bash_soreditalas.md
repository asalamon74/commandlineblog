---
layout: post
title: 'bash soreditálás'
permalink: https://commandline.blog.hu/2010/04/23/bash_soreditalas
post_id: 1926893
categories: 
- vi
- bash
- emacs
---

Ha a shellben elkezdünk egy parancssort gépelni, valójában egy egy soros kis editort használunk. Alapesetben 
[emacs](http://www.gnu.org/software/emacs/) üzemmódban, vagyis az emacs billentyűkombinációit használhatjuk. A következő táblázat a legfontosabbakat tartalmazza (meta többnyire az alt billentyű): 
ctrl-a             
sor elejére ugrás         
ctrl-e             
sor végére ugrás         
ctrl-b             
egy karakterrel balra ugrás         
ctrl-f             
egy karakterrel jobbra ugrás         
         
meta-b             
egy szóval balra ugrás         
meta-f             
egy szóval jobbra ugrás         
ctrl-w             
utolsó (kurzor előtti) szó törlése         
ctrl-u             
kurzortól balra minden törlése         
ctrl-k             
kurzortól jobbra minden törlése         
ctrl-y             
utolsónak törölt rész beillesztése         
ctrl-_             
undo 
  
Ha véletlenül nem ez az üzemmód lenne aktív, akkor a```
set -o emacs
```parancs segítségével váltatunk az emacs üzemmódra. Ha emacs helyett inkább 
[vi](http://szabilinux.hu/vi/index.html)-t választanánk, akkor a```
set -o vi
```segíthet.