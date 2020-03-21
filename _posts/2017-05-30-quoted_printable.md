---
layout: post
title: 'Quoted Printable'
permalink: /2017/05/30/quoted_printable
post_id: 12547851
categories: 
- perl
- mailbox
- recode
- qpd
- quotedprintable
---

Ősrégi 
[unix mailbox](https://en.wikipedia.org/wiki/Mbox) fájlokat szerettel volna egyszerűen megnézni parancssorban, de ezekben az ékezetes betűk (többnyire) Quoted Printable formátumban vannak, ami eléggi nehezíti az olvashatóságot (pl. cs=FCt=F6rt=F6k).

A következő egyszerű alias segít nagyon sokat:

```
$ alias qpd='perl -MMIME::QuotedPrint -pe '\''$_=MIME::QuotedPrint::decode($_);'\'''
```

 Ezután less helyett qpd-vel lehet belenézni a fájlokba:

```
qpd sent-mail-sep-2003
```

pontosabban mivel akkoriban még nem UTF8-at használtam, jól jön 
[recode](/2010/03/26/recode)is:

```
qpd sent-mail-sep-2003 | recode latin2..utf8
```

forrás: 
[https://gist.github.com/jjarmoc/1571540](https://gist.github.com/jjarmoc/1571540)