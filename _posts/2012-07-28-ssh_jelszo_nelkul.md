---
layout: post
title: 'ssh jelszó nélkül'
permalink: /2012/07/28/ssh_jelszo_nelkul
post_id: 4674338
categories: 
- ssh
- rsa
---

Általában persze nagyon hasznos, hogy ha egy távoli gépre be akarunk lépni ssh-val, akkor jelszót kell megadnunk, de ha egy scriptet írunk, akkor nagyon kényelmetlen ha futás közben megáll a script és jelszót kérdez.

ssh-keygen és ssh-copy-id használatával jelszó nélkül is be tudunk lépni a távoli gépre. Először is RSA kulcsokat gyártunk ssh-keygennel a host gépen ( ahonnan be szeretnénk lépni ), majd átmásoljuk a publikus kulcsot a távoli gépre ( ahová be szeretnénk lépni ):



```
$ 
**ssh-keygen**
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/user/.ssh/id_rsa.
Your public key has been saved in /home/user/.ssh/id_rsa.pub.
The key fingerprint is:
b2:46:91:0d:83:de:7a:e7:1a:b5:3a:9d:11:0a:96:99 user@host.akarmi.hu
The key's randomart image is:
+--[ RSA 2048]----+
|   E= ..         |
|...o.=           |
|.o.=o.o          |
|  + *.           |
|   = +o S        |
|  o =.S o        |
| . +  o          |
| o .             |
|                 |
+-----------------+
$ 
**ssh-copy-id -i ~/.ssh/id_rsa.pub tavoliuser@tavoligep.akarmi.hu**
29
tavoliuser@tavoligep.akarmi.hu's password: 
Now try logging into the machine, with "ssh 'tavoliuser@tavoligep.akarmi.hu'", and check in:
  .ssh/authorized_keys
to make sure we haven't added extra keys that you weren't expecting.
```

forrás: 
[http://www.thegeekstuff.com/2008/11/3-steps-to-perform-ssh-login-without-password-using-ssh-keygen-ssh-copy-id/](http://www.thegeekstuff.com/2008/11/3-steps-to-perform-ssh-login-without-password-using-ssh-keygen-ssh-copy-id/)