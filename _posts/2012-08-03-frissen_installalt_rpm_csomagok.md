---
layout: post
title: 'Frissen installált rpm csomagok'
permalink: https://commandline.blog.hu/2012/08/03/frissen_installalt_rpm_csomagok
post_id: 4683123
categories: 
- rpm
---

Sikerült túl sok backportolt csomagot felinstallálnom, így megbízhatatlanná vált a gépem. Ahhoz, hogy kijavítsam a hibát, szükségem volt a frissen installált rpm csomagok listájára:

```
rpm -qa --queryformat '%{installtime} %{name}-%{version}-%{release} %{installtime:date}\n' | sort -n +1 | sed -e 's/^[^ ]* //'
```

A script az öszes installált csomagot kilistázza időrendben, így elég a lista végét nézni.

forrás: 
[http://www.rpm.org/max-rpm/s1-rpm-query-handy-queries.html](http://www.rpm.org/max-rpm/s1-rpm-query-handy-queries.html)