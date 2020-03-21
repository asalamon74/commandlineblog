---
layout: post
title: 'dmidecode'
permalink: /2011/04/14/dmidecode
post_id: 2823073
categories: 
- hardver
- dmidecode
---

A 
```
dmidecode
```
 program segítségével számítógépünk hardvereiről kaphatunk igen részletes információt. Lehetőségünk van egy adott típusú hardver adatainak lekérdezésére, ha pl. csak a processzorról kell adat: 
```
[]$ dmidecode --type processor
 # dmidecode 2.10
 SMBIOS 2.3 present.
 
 Handle 0x0400, DMI type 4, 32 bytes
 Processor Information
         Socket Designation: Microprocessor
         Type: Central Processor
         Family: Pentium 4
         Manufacturer: Intel
         ID: 41 0F 00 00 FF FB EA BE
         Signature: Type 0, Family 15, Model 4, Stepping 1
         Flags:
                 FPU (Floating-point unit on-chip)
                 VME (Virtual mode extension)
                 DE (Debugging extension)
                 PSE (Page size extension)
                 TSC (Time stamp counter)
                 MSR (Model specific registers)
                 PAE (Physical address extension)
                 MCE (Machine check exception)
                 CX8 (CMPXCHG8 instruction supported)
                 APIC (On-chip APIC hardware supported)
                 SEP (Fast system call)
                 MTRR (Memory type range registers)
                 PGE (Page global enable)
                 MCA (Machine check architecture)
                 CMOV (Conditional move instruction supported)
                 PAT (Page attribute table)
                 PSE-36 (36-bit page size extension)
                 CLFSH (CLFLUSH instruction supported)
                 DS (Debug store)
                 ACPI (ACPI supported)
                 MMX (MMX technology supported)
                 FXSR (Fast floating-point save and restore)
                 SSE (Streaming SIMD extensions)
                 SSE2 (Streaming SIMD extensions 2)
                 SS (Self-snoop)
                 HTT (Hyper-threading technology)
                 TM (Thermal monitor supported)
                 PBE (Pending break enabled)
         Version: Not Specified
         Voltage: 1.8 V
         External Clock: 533 MHz
         Max Speed: 4000 MHz
         Current Speed: 2800 MHz
         Status: Populated, Enabled
         Upgrade: ZIF Socket
         L1 Cache Handle: 0x0700
         L2 Cache Handle: 0x0701
         L3 Cache Handle: Not Provided
```
   
Ha paraméter nélkül indítjuk el, akkor az összes hozzáférhető információt megkapjuk. 
 