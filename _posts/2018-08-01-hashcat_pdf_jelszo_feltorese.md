---
layout: post
title: 'hashcat: pdf jelszó feltörése'
permalink: /2018/08/01/hashcat_pdf_jelszo_feltorese
post_id: 14146789
categories:  []
---

Gyártsunk egy 
[jelszóvédett pdf](/2015/11/20/pdf_jelszovedelem)-et:

```
$ echo -n titok > titok.txt
$ enscript -p titok.{ps,txt}
$ ps2pdf titok.{ps,pdf}
$ pdftk titok.pdf output titok_jelszo.pdf user_pw 987654321
```

Ahhoz, hogy a titkosított pdf-et 
[hashcattel](/2018/07/29/hashcat) feltörhessük, két dologra lesz szükségünk. Először is tudnunk kell, milyen hash-et használ a pdf titkosítás. A pdf fájl elején látszik, hogy ez egy PDF 1.4-es fájl, 
```
hashcat --help
```
 alapján ez a 10500-as hash mód. Másrészt ki kell vágnunk a pdf fájlból a hash-t. Ezt a 
[JohnTheRipper](https://github.com/magnumripper/JohnTheRipper) program 
```
pdf2john.pl
```
 scriptjével tehetjük meg:

```
$ pdf2john.pl titok_jelszo.pdf | sed "s/^.*://" > hash_pdf.txt
```

Ezután hashcat már képes feltörni a jelszót brute-force módszerrel:

```
$ hashcat -m 10500 -a 3 -i hash_pdf.txt ?d?d?d?d?d?d?d?d?d?d?d
...

$pdf$2*3*128*-3904*1*16*35b780a117d0e708d9a5bc500c94dc31*32*5ec779d797699b837f97b6f33418f45400000000000000000000000000000000*32*240ab525f81f9d2851d51f167d556bb19f5bae85a6ca52e8c98a90fa98c2b65c:987654321
 
Session..........: hashcat
Status...........: Cracked
Hash.Type........: PDF 1.4 - 1.6 (Acrobat 5 - 8)
Hash.Target......: $pdf$2*3*128*-3904*1*16*35b780a117d0e708d9a5bc500c9...c2b65c
Time.Started.....: Sat Jul 28 11:29:47 2018 (1 min, 14 secs)
Time.Estimated...: Sat Jul 28 11:31:01 2018 (0 secs)
Guess.Mask.......: ?d?d?d?d?d?d?d?d?d [9]
Guess.Queue......: 9/11 (81.82%)
Speed.Dev.#2.....: 94665 H/s (28.31ms) @ Accel:16 Loops:8 Thr:64 Vec:1
Speed.Dev.#3.....: 1357.0 kH/s (68.98ms) @ Accel:640 Loops:17 Thr:64 Vec:1
Speed.Dev.#*.....: 1451.7 kH/s
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 107274240/1000000000 (10.73%)
Rejected.........: 0/107274240 (0.00%)
Restore.Point....: 10493952/100000000 (10.49%)
Candidates.#2....: 963454321 -> 999592321
Candidates.#3....: 962478232 -> 935512321

 Started: Sat Jul 28 11:28:21 2018
Stopped: Sat Jul 28 11:31:02 2018
```

Itt is feltételeztem persze, hogy csupa számjegyből állt a jelszó, így pár perc alatt megtalálta a program a jelszót. Enélkül persze sokkal tovább tartott volna.

 