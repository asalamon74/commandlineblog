---
layout: post
title: 'shellcheck'
permalink: /2018/09/11/shellcheck
post_id: 14229069
categories:  []
---

Még a 
[Shell Scripts Matter](/2017/06/13/cikkajanlo_shell_scripts_matter) cikk ajánlotta a 
[shellcheck](https://www.shellcheck.net/)et, de önmagában is megér egy bejegyzést.

Készítsünk egy nagyon egyszerű scriptet (test1.sh):

```
#!/bin/bash
echo hello $1
```

Ha elkezdjük használni, elég sokáig úgy viselkedik ahogy elvárjuk, de azért az utolsó két parancs közti különbség elsőre meglepő:

```
$ ./test1.sh a
hello a
$ ./test1.sh a b
hello a
$ ./test1.sh "a b"
hello a b
$ ./test1.sh "a* b"
hello a* b
$ ./test1.sh "t* b"
hello test1.sh test2.sh b
```

Egy ilyen rövid scriptben persze könnyen megtalálhatjuk a hibát, de sokkal egyszerűbb a scriptjeinket shellcheckkel ellenőriztetni:

```
$ shellcheck test1.sh

In test1.sh line 2:
echo hello $1
           ^-- SC2086: Double quote to prevent globbing and word splitting.
```

Ezután már egyértelmű  a javítás (test2.sh):

```
#!/bin/bash
echo hello "$1"
```

A script úgy működik, ahogy elvárható:

```
$ ./test2.sh a
hello a
$ ./test2.sh a b
hello a
$ ./test2.sh "a b"
hello a b
$ ./test2.sh "a* b"
hello a* b
$ ./test2.sh "t* b"
hello t* b
```

 