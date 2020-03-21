---
layout: post
title: 'XML fájlok összehasonlítása'
permalink: /2015/07/21/xml_fajlok_osszehasonlitasa
post_id: 7641144
categories: 
- xml
- diff
- xmllint
---

Ha XML fájlokat kell összehasonlítanom, akkor a 
[diff](/2011/09/04/diff_1)nem mindig túl hasznos, főleg ha nem én gyártottam az összehasonlítandó XML-eket. Egyrészt előfordul, hogy az XML gyártásnál nem használnak sortörést, másrészt pl. az attributumok sorrendje sem feltétlenül fix. 
[Process helyettesítés](/2011/09/07/diff_process_helyettesites) és 
[xmllint](http://xmlsoft.org/xmllint.html) segítségével már jobban össze lehet hasonlítani az XML fájlokat:

```
$ diff <(xmllint --exc-c14n file1.xml | xmllint --format -) <(xmllint --exc-c14n file2.xml | xmllint --format -)
```