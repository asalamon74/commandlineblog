---
layout: post
title: 'youtube-dl'
permalink: /2013/04/26/youtube-dl
post_id: 5247035
categories: 
- youtube
- mplayer
- youtube-dl
---

Több módszer is van aminek segítségével letölthetünk egy youtube videót, természetesen megoldható ez parancssorból is a 
[youtube-dl](http://rg3.github.io/youtube-dl/) program segítségével.

Miután felinstalláltam, először is frissítenem kellett a programot ( kétszer egymás után ):

```
youtube-dl --update
```

Ezután a letöltés már elég egyszerű:

```
youtube-dl "https://www.youtube.com/watch?v=OpaiGYxkSuQ"
```

A program képes egy félbemaradt letöltést folytatni, és youtube listákat is letölthetünk vele:

```
$ youtube-dl https://www.youtube.com/playlist?list=PLBDA2E52FB1EF80C9
[youtube] PL PLBDA2E52FB1EF80C9: Downloading page #1
[download] Downloading playlist: World History
[youtube:playlist] playlist 'World History': Collected 42 video ids (downloading 42 of them)
[download] Downloading video #1 of 42
...
```



Ha valójában nem elmenteni akarjuk a videót, csak a böngészőbe ágyazott flash player helyett a saját médialejátszónkat szeretnénk használni, akkor azt is megtehetjük:

```
mplayer -fs $(youtube-dl -g "https://www.youtube.com/watch?v=OpaiGYxkSuQ")
```

A -g kapcsoló miatt nem kell megvárni a teljes letöltést, hanem már közben is nézhetjük a videót.

Nevével ellentétben youtube-dl nemcsak youtube-ról tud letölteni, 
[itt](http://rg3.github.io/youtube-dl/documentation.html#d4) a támogatott oldalak listája.