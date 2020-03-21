---
layout: post
title: 'identify - Információk képekről'
permalink: /2010/05/23/identify_informaciok_kepekrol
post_id: 2004486
categories: 
- imagemagick
- digitális_fénykép
- identify
---

Korábban már többször említettem az 
[ImageMagick](http://www.imagemagick.org/) programcsomagot, pontosabban annak 
[convert](http://www.imagemagick.org/script/convert.php) programját. Most ImageMagick egy másik parancssoros programjára hívnám fel a figyelmet. 
Az 
[identify](http://www.imagemagick.org/script/identify.php) parancs segítségével egy képfájlról kaphatunk információt. Ez nem egyszerűen az 
[EXIF információkat](http://commandline.blog.hu/2010/05/14/exiftool) jelenti, hanem annál sokkal bővebb információhalmazt: 
```
[gep]$ identify -verbose 38110037.tif
 Image: 38110037.tif
   Format: TIFF (Tagged Image File Format)
   Class: DirectClass
   Geometry: 3089x2048+0+0
   Resolution: 72x72
   Print size: 42.9028x28.4444
   Units: PixelsPerInch
   Type: TrueColor
   Base type: TrueColor
   Endianess: MSB
   Colorspace: RGB
   Depth: 8-bit
   Channel depth:
     red: 8-bit
     green: 8-bit
     blue: 8-bit
   Channel statistics:
     red:
       min: 0 (0)
       max: 255 (1)
       mean: 181.971 (0.713612)
       standard deviation: 58.2179 (0.228305)
       kurtosis: 1.31905
       skewness: -1.54975
     green:
       min: 0 (0)
       max: 255 (1)
       mean: 179.265 (0.703002)
       standard deviation: 61.8661 (0.242612)
       kurtosis: 0.52021
       skewness: -1.24466
     blue:
       min: 0 (0)
       max: 255 (1)
       mean: 171.985 (0.67445)
       standard deviation: 67.8177 (0.265952)
       kurtosis: -0.312623
       skewness: -0.728281
   Image statistics:
     Overall:
       min: 0 (0)
       max: 255 (1)
       mean: 133.305 (0.522766)
       standard deviation: 94.2908 (0.369768)
       kurtosis: -1.49699
       skewness: -0.408584
   Rendering intent: Undefined
   Interlace: None
   Background color: white
   Border color: rgb(223,223,223)
   Matte color: grey74
   Transparent color: black
   Compose: Over
   Page geometry: 3089x2048+0+0
   Dispose: Undefined
   Iterations: 0
   Compression: None
   Orientation: TopLeft
   Properties:
     comment: IslBG
     date:create: 2010-05-15T08:24:45+02:00
     date:modify: 2010-05-15T08:24:45+02:00
     signature: 8944ac14da7f3604c0e2681b1dc3a5845466d816e76d03c46161d425f518d354
     tiff:photometric: RGB
     tiff:rows-per-strip: 1
     tiff:software: IslBG
   Artifacts:
     verbose: true
   Tainted: False
   Filesize: 18.12MiB
   Number pixels: 6.033MiB
   Pixels per second: 33.52MiB
   User time: 0.110u
   Elapsed time: 0:01.179
   Version: ImageMagick 6.5.7-0 2009-10-22 Q16 http://www.imagemagick.org
```
  