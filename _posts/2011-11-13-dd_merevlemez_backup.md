---
layout: post
title: 'dd (merevlemez backup)'
permalink: /2011/11/13/dd_merevlemez_backup
post_id: 3372891
categories: 
- backup
- mount
- merevlemez
- dd
- fdisk
---

A 
[DVD-hez](http://commandline.blog.hu/2010/01/10/dd_dvd_backup) hasonló módon egy teljes merevlemezről is készíthetünk biztonsági mentést:

```
dd if=/dev/sda of=hdd_image.img
```

Ebben az esetben az adatok elérése kissé bonyolultabb, hiszen a mount parancs segítségével nem teljes merevlemezt, hanem partíciót érünk el, így ki kell számolnunk, hol is kezdődnek a partíciók. Az fdisk parancs segítségével kaphatunk információt:

```
# fdisk -lu hdd_image.img 
Disk hdd_image.img: 80.0 GB, 80026361856 bytes
240 heads, 63 sectors/track, 10337 cylinders, total 156301488 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x92e474f4
        Device Boot      Start         End      Blocks   Id  System
hdd_image.img1   *          63   138907439    69453688+   7  HPFS/NTFS/exFAT
hdd_image.img2       138907440   156295439     8694000    c  W95 FAT32 (LBA)
```

 Mivel fdisk a fenti esetben 512 byte-os egységekben számol, ezért a 2. partíció a 138907440*512. byte-on kezdődik. Vagyis a következő paranccsal érhetjük el a 2. partíciót:

```
 mount -o loop,offset=$((138907440*512)) hdd_image.img /mnt/test
```

Az fdisk-et is tartalmazó util-linux-ng csomag 2.17-es verziójában nem működött rendesen a fenti módszer, 2.19-re kellett frissítenem.