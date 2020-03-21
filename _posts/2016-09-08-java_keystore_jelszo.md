---
layout: post
title: 'java keystore jelszó'
permalink: /2016/09/08/java_keystore_jelszo
post_id: 11687825
categories: 
- java
- jelszó
- brute_force
- keystore
- keytool
---

Generáltam egy java keystore-t, benne egy kulcspárral:

```
keytool -genkey -noprompt -alias mydomain -keyalg RSA -keystore test_keystore.jks -keysize 2048 -dname "CN=commandline.blog.hu, C=HU" -storepass 123456  -keypass jelszo
```

A keystore jelszava 123456 a kulcspáré jelszo.

## Brute force


Elég sok eszköz van, amivel brute force támadással megpróbálhatjuk feltörni a keystore jelszavát, én a 
[keystorebreaker](https://github.com/meefik/keystorebreaker)t próbáltam ki, itt megadhatjuk milyen karakterek fordulhatnak elő a jelszóban. A legfeljebb 6 karakter hosszú csak számokat tartalmazó jelszavakat pillanatok alatt végigpróbálja:

```
java -jar KeystoreBreaker.jar test_keystore.jks 0123456789 000000 999999 4
```

Ehhez a feltöréséhez pár másodperc elég volt. Nyilván több idő kell ha nemcsak számok lehetnek a jelszóban, a legfeljebb 6 hosszú szám+kisbetű összes lehetőségének végigpróbálásához a program szerint 1.5 óra kellene, szám+kisbetű+nagybetűnél kb. 2 nap.

Itt tartottam a bejegyzéssel, ide jönne a rész ami leírja, hogy milyen jelszót (ne) válasszunk, amikor találtam még valamit.

## Changepassword


 A changepassword nevű programmal egy keystore jelszavát változtathatjuk meg. Megkérdi a régi jelszót, az újat és létrehoz egy új keystore-t az új jelszóval ami a régi kulcsait tartalmazza:

```
$ java ChangePassword test_keystore.jks test_keystore2.jks
Enter keystore password: fogalmamsincs
Changing password on 'test_keystore.jks', writing to 'test_keystore2.jks'...
Enter new keystore password: ujjelszo
```

Egy igen furcsa van a programban, nagyszerűen működik akkor is, ha rossz jelszót adunk meg. A programot 
[innen](https://gist.github.com/zach-klippenstein/4631307) töltöttem le, élesben nem próbáltam ki, de a fenti egyszerű teszt alapján működik. A szerző alapján a kulcspár jelszavát nem lehet így lecserélni, az valóban biztonságos.

Titkon azért abban bízom én értettem valamit félre valamit és nem ennyire rossz a java keystore jelszókezelése.