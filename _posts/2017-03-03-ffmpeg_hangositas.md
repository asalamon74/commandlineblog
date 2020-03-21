---
layout: post
title: 'ffmpeg hangosítás'
permalink: /2017/03/03/ffmpeg_hangositas
post_id: 12309081
categories: 
- audio
- hangosítás
- ffmpeg
---

Ha túl halk egy videónk, a következőképpen hangosíthatjuk fel egyszerűen:

Először is elemeztetjuk ffmpeggel a hangsávot:

```
$ ffmpeg -i input.mp4 -af "volumedetect" -f null /dev/null
[Parsed_volumedetect_0 @ 0x18157c0] n_samples: 349184
[Parsed_volumedetect_0 @ 0x18157c0] mean_volume: -24.5 dB
[Parsed_volumedetect_0 @ 0x18157c0] max_volume: 
**-9.5**
 dB
[Parsed_volumedetect_0 @ 0x18157c0] histogram_9db: 13
[Parsed_volumedetect_0 @ 0x18157c0] histogram_10db: 28
[Parsed_volumedetect_0 @ 0x18157c0] histogram_11db: 179
[Parsed_volumedetect_0 @ 0x18157c0] histogram_12db: 513
```

Ez elég sok mindent kiír, vastaggal jelöltem a számunkra lényeges értéket. Ezután ezt ez értéket felhasználva felhangosíthatjuk a videót:

```
ffmpeg -i input.mp4 -af "volume=9.5dB" -vcodec copy -acodec libvo_aacenc -b:a 192k output.mp4
```

Nyilván ez egy igen egyszerű módszer, lehet ennél sokkal jobb módszereket is találni, de az esetek többségében nekem ez pont elég.

Forrás:
[http://superuser.com/a/323127/8240](http://superuser.com/a/323127/8240)