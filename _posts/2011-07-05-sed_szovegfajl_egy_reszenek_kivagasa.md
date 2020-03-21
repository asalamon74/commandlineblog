---
layout: post
title: 'sed: szövegfájl egy részének kivágása'
permalink: /2011/07/05/sed_szovegfajl_egy_reszenek_kivagasa
post_id: 3039131
categories: 
- sed
- reguláris_kifejezés
---

Ha van egy szövegfájlokkal kapcsolatos problémám, akkor többnyire segít a 
[sed](http://hu.wikipedia.org/wiki/Sed) és a reguláris kifejezés (
[persze nem mindig](http://regex.info/blog/2006-09-15/247)). 
Egy szövegfájlból kellett egy részletet kivágnom. Reguláris kifejezéssel határoztam meg az első sort ami kellett nekem, egy másik reguláris kifejezéssel az utolsó sort. Ezután a következő módon lehet a két reguláris kifejezés közti részt megkapni: 
```
sed -n '/STARTREGEXP/,/ENDREGEXP/p' file.txt
``` 
  
 