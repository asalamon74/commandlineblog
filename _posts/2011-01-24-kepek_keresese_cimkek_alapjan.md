---
layout: post
title: 'Képek keresése címkék alapján'
permalink: /2011/01/24/kepek_keresese_cimkek_alapjan
post_id: 2549140
categories: 
- címke
- exif
- exiftool
---

Ahogy egyre több digitális fényképet tárolunk, egyre nehezebb a fényképek rendszerezése. Segít (valamit) a káoszon, ha a képekhez címkéket rendelünk hozzá. A címkék az exif információk között tárolódnak, a Keywords tag alatt. Ha szorgalmasan felcímkéztük a képeket, akkor időnként keresni is kell a címkék között. A következő script segítségével ezt könnyen megtehetjük: 
```
find . -name "*.jpg" -print0 | xargs -0 -n1 exiftool -m -p '$directory/$filename: $Keywords' | grep -i kutya
```