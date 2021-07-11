---
layout: post
title: 'suspend deep sleep S3'
excerpt: 'suspend deep sleep javítás ACPI DSDT hack'
permalink: /2021/07/11/suspend_deep_sleep
categories: []
---
Meghalt a laptopom, így vettem egy újat, és meglepve láttam, hogy a Dell Vostro 3500 alvás (suspend) közben túl sok áramot fogyaszt. AlmaLinux-ot használok, ez lényegében a CentOS utóda szeretne lenni.
A leírások alapján `s2idle`-ről kell `deep`-re állítani az alvási módot. Azonban nálam nincs is lehetőség erre, a laptop nem támogatja ezt:

```
$ cat /sys/power/mem_sleep
[s2idle]
$ sudo dmesg | grep -i acpi | grep supports
[    0.307096] ACPI: (supports S0 S4 S5)
[    0.328747] acpi PNP0A08:00: _OSC: OS supports [ExtendedConfig ASPM ClockPM Segments MSI HPX-Type3]
```

Az `S3` állapot a deep sleep, ez nem szerepel a támogatott módok között. (Az `S2` sincsen, de `s2idle`-hez nem `S2` kell, hanem `S0ix`).
A Dell fórumán találtam rengeteg [szálat]("https://www.dell.com/community/XPS/Ubuntu-deep-sleep-missing-for-xps-9310/m-p/7947197")
ahol erre panaszkodtak linuxosok (és néha Windowsosok is), de igazi megoldást nem adott a Dell.
Némelyik laptopnál BIOS-ban be lehet ezt állítani, de én nem találtam ilyen lehetőséget (van egy deep sleep kapcsoló, de az már be van kapcsolva).

### ACPI DSDT hack

Meg lehet hackelni ezt az ACPI DSDT táblájának módosításával:

```
$ mkdir acpi
$ cd acpi
$ acpidump -b # created lots of files
$ iasl -e *.dat -d dsdt.dat
$ iasl -tc dsdt.dsl &> iasl_errors.txt
```

Kiolvassuk az ACPI adatokat, disassembler segítségével készítünk egy `dsdt.dsl` fájl, majd megpróbáljuk lefordítani. 

#### dsdt.dsl módosítás

Valamiért teljesen általános, hogy
itt hibát kapunk, nálam ez volt a hiba:

```
Compiler aborting due to parser-detected syntax error(s)
dsdt.dsl   4331:                     ECRW (If (PM0H)
Error    6126 -                            ^ syntax error, unexpected PARSEOP_IF, expecting PARSEOP_CLOSE_PAREN or ','

dsdt.dsl   4332:                             {
Error    6126 -                             ^ syntax error, unexpected '{'

dsdt.dsl   4335:                             }) = Zero
Error    6126 -                              ^ syntax error, unexpected PARSEOP_CLOSE_PAREN
```

Ezt megjavítottam azzal, hogy a fájlban ezt a részt:

```
If ((PM6H == One))
{
    CreateBitField (BUF0, \_SB.PC00._Y0C._RW, ECRW)  // _RW_: Read-Write Status
    ECRW (If (PM0H)
            {
                CreateDWordField (BUF0, \_SB.PC00._Y0D._LEN, F0LN)  // _LEN: Length
                F0LN = Zero
            }) = Zero
}
```

átírtam erre:

```
If (PM0H)
{
    CreateDWordField (BUF0, \_SB.PC00._Y0D._LEN, F0LN)  // _LEN: Length
    F0LN = Zero
}

If ((PM0H == One))
{
    CreateBitField (BUF0, \_SB.PC00._Y0D._RW, F0RW)  // _RW_: Read-Write Status
    F0RW = Zero
}
```

Ezután a fordítási hiba eltűnt, és a nem sokkal megnyugtatóbb `0 Errors, 188 Warnings` üzenet jelent meg.

Rákeresve S3-ra, vagy egy ilyen rész a fájlban:

```
If (SS3)
    {
        Name (_S3, Package (0x04)  // _S3_: S3 System State
        {
            0x05,
            Zero,
            Zero,
            Zero
        })
    }
```

Ez alapján úgy tűnik van egy `SS3` változó valahol. És valóban van egy ilyen rész is:

```
   Name (SS3, Zero)
```

Ezt elegánsan átírtam erre:

```
   Name (SS3, One)
```

Ezen kívül verziószámot is kell növelni, így ezt a sort

```
DefinitionBlock ("", "DSDT", 2, "DELL  ", "Dell Inc", 0x00000002)
```

erre írtam át:

```
DefinitionBlock ("", "DSDT", 2, "DELL  ", "Dell Inc", 0x00000003)
```

Ezután lefordítottam a fájlt és készítettem egy  `acpi_override` fájl:

```
$ iasl -ve -tc dsdt.dsl
Intel ACPI Component Architecture
ASL+ Optimizing Compiler/Disassembler version 20180629
Copyright (c) 2000 - 2018 Intel Corporation

ASL Input:     dsdt.dsl - 76805 lines, 2526115 bytes, 43265 keywords
AML Output:    dsdt.aml - 362899 bytes, 5619 named objects, 37646 executable opcodes
Hex Dump:      dsdt.hex - 3402617 bytes

Compilation complete. 0 Errors, 188 Warnings, 241 Remarks, 487 Optimizations
$ mkdir -p kernel/firmware/acpi
$ cp dsdt.aml kernel/firmware/acpi
$ find kernel | cpio -H newc --create > acpi_override
711 blocks
```

#### kernel

Ahhoz, hogy a kernel használja is ezt a fájlt, előszöt is `/etc/default/grub`-t módosítottam:

```
GRUB_CMDLINE_LINUX_DEFAULT="..... mem_sleep_default=deep"
GRUB_EARLY_INITRD_LINUX_CUSTOM="acpi_override"
```

A következő parancs frissíti a grub config fált:

```
$ grub2-mkconfig -o "$(readlink -e /etc/grub2-efi.cfg)"
```

De ez még mindig nem elég, a `/boot/loader/entries/` alkönyvtárban a megfelelő kernelnél is kell módosítani egy sort:

```
initrd /acpi_override /initramfs-5.12.13-1.el8.elrepo.x86_64.img $tuned_initrd
```

#### boot után

Boot után látszik, hogy a rendszer használja a javított DSDT-t és S3 elérhető:

```
$ dmesg | grep -i DSDT
[    0.007916] ACPI: DSDT ACPI table found in initrd [kernel/firmware/acpi/dsdt.aml][0x58993]
[    0.007983] ACPI: Table Upgrade: override [DSDT-DELL  -Dell Inc]
[    0.007985] ACPI: DSDT 0x0000000063F99000 Physical table override, new table: 0x000000005A704000
[    0.007986] ACPI: DSDT 0x000000005A704000 058993 (v02 DELL   Dell Inc 00000003 INTL 20180629)
[    0.008046] ACPI: Reserving DSDT table memory at [mem 0x5a704000-0x5a75c992]
[    0.310576] ACPI: \_SB_.PC00.LPCB.ECDV: Boot DSDT EC used to handle transactions
[    0.369005] ACPI: \_SB_.PC00.LPCB.ECDV: Boot DSDT EC initialization complete
$ dmesg | grep -i acpi | grep supports
[    0.310624] ACPI: (supports S0 S3 S4 S5)
[    0.330464] acpi PNP0A08:00: _OSC: OS supports [ExtendedConfig ASPM ClockPM Segments MSI HPX-Type3]
$ cat /sys/power/mem_sleep
s2idle [deep]
```

És a laptop alvás közben tényleg sokkal kevesebb áromot fogyaszt.

_Azt hozzá kell tennem, hogy a géphez adott gyári Ubuntuban sincsen S3 támogatás, és az mégsem fogyaszt annyi áramot alvás közben,
Valószínűleg az Ubuntu 5.10 OEM kernelében benne vannak azok a javítások, amelyek hiányoznak az alap 5.12-es kernelből._

Hasznos cikkek a témában:
- <https://dev.to/epassaro/fix-suspend-issues-on-dell-7405-2-in-1-3l1b>
- <https://wiki.archlinux.org/title/DSDT>
- <http://stens4104.blogspot.com/2021/03/>

