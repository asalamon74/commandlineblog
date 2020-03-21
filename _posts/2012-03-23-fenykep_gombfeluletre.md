---
layout: post
title: 'Fénykép gömbfelületre'
permalink: https://commandline.blog.hu/2012/03/23/fenykep_gombfeluletre
post_id: 4332484
categories: 
- gömb
- digitális_fénykép
---

A photo.stackexchange oldalon tette fel valaki a 
[kérdés](http://photo.stackexchange.com/q/17321/507)t, miként lehet egy fényképet úgy kinyomtatni, hogy gömbfelületre lehessen felragasztani a képet.

Az 
[IP-Slicer](http://www.bruno.postle.net/2001/ip-slicer/) perl script segítségével oldaható meg a feladat:

```
sphere-slicer.pl 12 1500 sampleimage.jpg
```

A fenti script 12 darabra vágja a képet úgy, hogy a az "egyenlítő" 1500 pixel hosszú lesz.
![input.jpg](http://m.blog.hu/co/commandline/image/input.jpg)

Az elkészült darabok:

![o1.png](http://m.blog.hu/co/commandline/image/o1.png) 
![o2.png](http://m.blog.hu/co/commandline/image/o2.png) 
![o3.png](http://m.blog.hu/co/commandline/image/o3.png) 
![o4.png](http://m.blog.hu/co/commandline/image/o4.png) 
![o5.png](http://m.blog.hu/co/commandline/image/o5.png) 
![o6.png](http://m.blog.hu/co/commandline/image/o6.png) 
![o7.png](http://m.blog.hu/co/commandline/image/o7.png) 
![o8.png](http://m.blog.hu/co/commandline/image/o8.png) 
![o9.png](http://m.blog.hu/co/commandline/image/o9.png) 
![o10.png](http://m.blog.hu/co/commandline/image/o10.png) 
![o11.png](http://m.blog.hu/co/commandline/image/o11.png) 
![o12.png](http://m.blog.hu/co/commandline/image/o12.png)