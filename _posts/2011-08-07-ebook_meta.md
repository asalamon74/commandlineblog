---
layout: post
title: 'ebook-meta'
permalink: /2011/08/07/ebook_meta
post_id: 3129994
categories: 
- ebook
- calibre
---

Bár az elektronikus könyveket kezelő 
[calibre](http://calibre-ebook.com/) alapvetően grafikus program, több funkciója parancssorból is használható. Az elektronikus könyvek metaadatait az 
```
ebook-meta
```
 programmal olvashatjuk ki, vagy módosíthatjuk. 
Alapesetben kiírja a könyv metaadatait: 
```
$ ebook-meta Doyle_Sherlock_Holmes_kalandjai.prc
 Title               : Sherlock Holmes kalandjai
 Author(s)           : Sir Arthur Conan Doyle
 Publisher           : Kindlevarázs
 Tags                : Classics
 Language            : hu
```
A borító kiolvasásához a 
```
--get-cover
```
 kapcsolót használhatjuk:  
```
ebook-meta Doyle_Sherlock_Holmes_kalandjai.prc --get-cover sherlock.jpg
``` 
A metaadatokat persze módosíthatjuk is. A borítót például a következő módon cserélhetjük le: 
```
ebook-meta Doyle_Sherlock_Holmes_kalandjai.prc --cover újborító.jpg
``` 
 