---
layout: post
title: '.src.rpm patchelése'
permalink: /2012/03/09/_src_rpm_patchelese
post_id: 4299120
categories: 
- patch
- rpm
---

Már írtam arról, miként tudunk 
[rpm-et készíteni .src.rpm](/2011/07/08/rpm_keszitese_src_rpm_bol)-ből, és arrról is, miként lehet egy programhoz 
[patchet készíteni](/2012/02/27/patch_keszitese). Most a két dolgot kötöm össze, vagyis azt írom le, miként lehet egy .src.rpm-et úgy lefordítani, hogy használja a saját patchünket.

Előkészületként érdemes a két lépést külön kipróbálni, vagyis arról is győződjünk meg, hogy működik a patchünk, és arról is, hogy patch nélkül le tudjuk fordítani a forrás rpm-et!

Először is installáljuk a .src.rpm-et:

```
rpm -ivh ufraw-0.18-4.src.rpm
```

Ennek hatására rpmbuild alkönyvtárunkban létrejönnek a következő fájlok, de a rendszer nem végzi el a fordítást:

```
SOURCES/ufraw-0.18.tar.gz
SPECS/ufraw.spec
```

A program forráskódját tartalmazó .tar.gz mellé másoljuk át a patchünket:

```
SOURCES/ufraw_kx.patch
```

Ezen kívül módosítanunk kell a .spec fájlt:

```
%define name            ufraw
%define version         0.18
%define release         %mkrel 4
**Patch0: ufraw_kx.patch**...
%prep
%setup -q
**%patch0 -p1**
```

A spec fájlnak csak a számunkra érdekes részét mutatom, a módosításokat kiemelve.

Ezután már lefordíthatjuk a .src.rpm-et:

```
rpmbuild -bb rpmbuild/SPECS/ufraw.spec
```