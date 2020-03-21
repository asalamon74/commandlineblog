---
layout: post
title: 'epubcheck'
permalink: https://commandline.blog.hu/2014/03/31/epubcheck
post_id: 5884236
categories: 
- epub
---

Ha epub fájlokat gyártunk, akkor nem elég ha 1-2 eszközön ellenőrizzük, hanem illik azt is vizsgálni, hogy megfelel-e a szabványnak.

Epub fájlokat validálhatunk az 
[epubcheck](https://github.com/IDPF/epubcheck) használatával:

```
$ java -jar epubcheck-3.0.1.jar little_brother_doctorow_cory.epub 
Epubcheck Version 3.0.1
Validating against EPUB version 2.0
ERROR: little_brother_doctorow_cory.epub/mimetype: Mimetype file should contain only the string "application/epub+zip".
ERROR: little_brother_doctorow_cory.epub/OPS/fb.opf(25,78): date value 'Mon May 05 20:23:43 +0200 2008' is not valid as per http://www.w3.org/TR/NOTE-datetime: [For input string: "Mon May 05 20"] is not an integer
WARNING: little_brother_doctorow_cory.epub/OPS/fb.ncx: meta@dtb:uid content '9bde0872-1ad5-11dd-b5b9-0018f369440e' should conform to unique-identifier in content.opf: 'urn:uuid:9bde0872-1ad5-11dd-b5b9-0018f369440e'
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(68,58): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(89,58): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(110,58): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(131,58): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(152,58): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(740,59): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(761,59): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(782,59): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(803,59): assertion failed: The "id" attribute does not have a unique value
ERROR: little_brother_doctorow_cory.epub/OPS/fb.ncx(824,59): assertion failed: The "id" attribute does not have a unique value
Check finished with warnings or errors
```

A program láthatóan igen szigorú, kipróbáltam pár hivatalos helyről származó epubbal, de mindegyikben talált kisebb-nagyobb hibát.