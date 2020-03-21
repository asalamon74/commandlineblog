---
layout: post
title: 'szkennelés'
permalink: https://commandline.blog.hu/2011/01/15/szkenneles
post_id: 2550224
categories: 
- szkennelés
- sane
- scanimage
---

Bár a szkennelés nem az a feladat amit feltétlenül parancssorból szeretnénk elvégezni, ha szükségünk van rá, 
[SANE](http://www.sane-project.org/) támogatja ezt is. 
Először is listázzuk ki az elérhető eszközöket: 
```
[]$ scanimage -L
 device `v4l:/dev/video0' is a Noname CNF8243 virtual device
 device `gt68xx:libusb:002:004' is a Mustek ScanExpress 1200 UB Plus flatbed scanner
```
 Az első eszköz a webkamera, amivel most nem foglalkozunk, a második egy valódi szkenner, amit használni szeretnénk. 
Először is listázzuk ki, pontosan milyen beállításokat támogat az eszköz: 
```
scanimage --help --device-name gt68xx:libusb:002:004
``` 
A 
```
--device-name
```
 kapcsolóra nincsen szükségünk abban az esetben ha az előző parancs csak egy eszközt listázott ki. Ha több eszközünk van, de az esetek többségében ugyanazt szeretnénk használni, akkor SANE_DEFAULT_DEVICE környezeti változóban beállíthatjuk az alapértelmezett eszközt. 
Eredményül egy elég hosszú leírást kapunk, aminek a közepén egy ilyen részt kell látnunk: 
```
Options specific to device `gt68xx:libusb:002:004':
   Scan Mode:
     --mode Color|Gray|Lineart [Gray]
         Selects the scan mode (e.g., lineart, monochrome, or color).
     --gray-mode-color Red|Green|Blue [Green]
         Selects which scan color is used gray mode (default: green).
     --source Flatbed|Transparency Adapter [inactive]
         Selects the scan source (such as a document-feeder).
     --preview[=(yes|no)] [no]
         Request a preview-quality scan.
     --depth 8|12 [8]
         Number of bits per sample, typical values are 1 for "line-art" and 8
         for multibit scans.
     --resolution 50|75|150|300|600|1200dpi [300]
         Sets the resolution of the scanned image.
 ...
``` 
Bár ezek az opciók eszköz-specifikusak az egyszerűbb kapcsolók megtalálhatóak szinte az összes szkennernél. 
Ezután a következő paranccsal szkennelhetünk be egy képet: 
```
scanimage --mode=color --resolution=300 --format=tiff --device-name gt68xx:libusb:002:004 > kep.tiff
```