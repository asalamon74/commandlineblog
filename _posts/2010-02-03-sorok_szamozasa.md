---
layout: post
title: 'Sorok számozása'
permalink: https://commandline.blog.hu/2010/02/03/sorok_szamozasa
post_id: 1673896
categories: 
- cat
- nl
- sorszámozás
---

Bár most nem jut eszembe mikor, de időnként hasznos ha egy fájl sorait megszámozzuk. Legegyszerűbben a 
```
cat
```
 paranccsal tehetjük ezt. Ha az összes sort meg szeretnénk számozni akkor a 
```
-n
```
, ha csak a nem üres sorokat, akkor a 
```
-b
```
 kapcsolót használhatjuk. 
```
# cat -n teszt.txt
      1    egy
      2    kettő
      3    három
      4    
      5    négy
      6    öt
      7    hat
      8    
      9    hét
```
  
 
```
# cat -b teszt.txt
      1    egy
      2    kettő
      3    három
 
      4    négy
      5    öt
      6    hat
 
      7    hét
``` 
Ha ennél bonyolultabb módon szeretnénk a sorokat megszámozni, akkor az 
```
nl
```
 parancs segíthet: 
```
# nl -w 3 -i 2 -v 2 -nrz teszt.txt
 002    egy
 004    kettő
 006    három
     
 008    négy
 010    öt
 012    hat
     
 014    hét
``` 
A fenti példában használat paraméterek jelentése: 
```
-w 3: Három számjegy a sorszám,
 -i 2: kettesével növekszik,
 -v 2: kettővel kezdődik,
 -nrz: jobbra igazítva, 0-k kiírva.
```