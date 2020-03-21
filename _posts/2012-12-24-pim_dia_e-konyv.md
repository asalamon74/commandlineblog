---
layout: post
title: 'PIM DIA e-könyv'
permalink: https://commandline.blog.hu/2012/12/24/pim_dia_e-konyv
post_id: 4976296
categories: 
- ebook
- dia
- calibre
- sed
---

A 
[DIA ( Digitális Irodalmi Akadémia )](http://www.pim.hu/dia) oldalán kortárs magyar írók műveit érhetjük el ingyen. Számomra nem teljesen érthető módon ezeket a műveket a weben elolvashatjuk, de arra már nincs mód ( legalábbis én nem találtam ), hogy valami e-könyv formátumban letölthessük őket.

Persze egy-két kattintással átkonvertálhatjuk a könyveket, a 
[Kindlevarázs](http://www.kindlevarazs.hu/kortarsak-a-konyvespolcra-dia-a-kindle-n/) írt egy elég részletes leírást erről. A leírás óta van már hivatalos 
[send to kindle](http://www.amazon.com/gp/sendtokindle) alkalmazás is, inkább azt érdemes használni.

A leírt nagyon egyszerű konverzió hátránya, hogy elvesznek a lábjegyzetek, és a könyv tele lesz szórva felesleges oldalszámokkal. Nem is beszélve arról, hogy az összes metaadat elveszik.

Mivel bosszantott a dolog, készítettem egy scriptet, ami elvégzi a konvertálást, és elfogadhatóbb eredményt ad. Tisztában vagyok vele, hogy a script egyértelműen a legrondább kódrészlet amit valaha a blogon írtam, és azzal is, hogy a reguláris kifejezések használatára nincsen mentség, viszont arra a pár könyvre amire kipróbáltam elég jól működött.

```
#!/bin/bash
FILE=`basename $1 .xhtml`
echo ${FILE}_1.xhtml
cat $FILE.xhtml | sed s@\<span\ class=\"oldaltores\"\>.*\</span\>@@ |\
 sed '/<a name="DIAPage.*>/{ N; s/<a name="DIAPage.*>[\n]// }' | sed 's@<div class="cim">\(.*\)</div>@<h1>\1</h1>@' > ${FILE}_conv.xhtml
ebook-convert ${FILE}_conv.xhtml ${FILE}.fb2
CIM=`sed -n 's@[ ]*<div class="konyvcim">\(.*\)</div>@\1@p' < ${FILE}_conv.xhtml`
SZERZO=`sed -n 's@[ ]*<div class="szerzo">\(.*\)</div>@\1@p' < ${FILE}_conv.xhtml`
VEZETEKNEV=`echo $SZERZO | cut -f 1 -d ' '`
KERESZTNEV=`echo $SZERZO | cut -f 2- -d ' '`
rm ${FILE}_conv.xhtml
sed 's@<sup>\*\(.*\)</sup>@<a xlink:href="#calibre_link-\1">\1</a>@' < ${FILE}.fb2 |\
sed 's@\*\(.*\)</p>@<p id="calibre_link-\1">\1</p></p>@' |\
sed "s@<first-name>[^/]*</first-name>@<first-name>$KERESZTNEV</first-name>@g" |\
sed "s@<lang>[^/]*</lang>@<lang>hu</lang>@g" |\
sed "s@<empty-line[ ].*/>@@g" |\
sed "s@<last-name>[^/]*</last-name>@<last-name>$VEZETEKNEV</last-name>@g" > ${FILE}_conv.fb2
rm ${FILE}.fb2
ebook-meta --cover=$2 ${FILE}_conv.fb2
ebook-convert ${FILE}_conv.fb2 ${FILE}.mobi
rm ${FILE}_conv.fb2
ebook-meta -t "${CIM}" -l hu --isbn "$3" ${FILE}.mobi
```

A scriptet neve dia_convert.sh. Ha a DIA-ról letöltünk egy könyvet XHTML formátumban ( input.xhtml ), kikeressük a borítót ( input.jpg ), majd megkeressünk az ISBN-számot ( példában: 1111111111 ), akkor a következő módon gyárthatjuk le a mobi fájlt:

```
dia_convert.sh input.xhtml input.jpg 11111111111
```

A script a sed indokolatlan használata mellett 
[calibre](http://calibre-ebook.com/)-re épül.