---
layout: post
title: 'systemd-analyze'
permalink: /2015/12/29/systemd-analyze
post_id: 8208402
categories: 
- boot
- systems
- systemd-analyze
---

Ha lassan bootol a számítógépünk, akkor systemd-analyze segítségével kaphatunk részletes információt. Lekérdezhetjük a bootolás hosszát:

```
$ systemd-analyze
Startup finished in 6.697s (kernel) + 20.050s (userspace) = 26.748s
```

Részletesen kilistázhatjuk, pontosan mi is indul lassan:

```
$ systemd-analyze blame
         12.849s network-up.service
          6.058s systemd-suspend.service
          2.023s mandriva-everytime.service
          1.909s shorewall6.service
          1.436s fedora-storage-init.service
          1.036s shorewall.service
          ...
```

Valójában persze a folyamatok részben párhuzamosan indulnak, így igazából akkor van csak gond, amikor egymásra épülő szolgáltatások tartják fel egymást:

```
$ systemd-analyze critical-chain 
The time after the unit is active or started is printed after the "@" character.
The time the unit takes to start is printed after the "+" character.
graphical.target @20.049s
└─multi-user.target @20.048s
  └─shorewall6.service @18.139s +1.909s
    └─network.target @18.137s
      └─network-up.service @5.286s +12.849s
        └─basic.target @5.285s
          └─mandriva-everytime.service @3.262s +2.023s
            └─local-fs.target @3.261s
              └─run-user-500-gvfs.mount @19.243s
                └─local-fs-pre.target @555ms
                  └─systemd-remount-fs.service @291ms +263ms
                    └─systemd-readahead-replay.service @216ms +67ms
```

Ha grafikusan szeretnénk áttekinteni a bootolás folyamatát:

```
systemd-analyze plot > plot.svg
```