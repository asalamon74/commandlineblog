---
layout: post
title: 'ssconvert'
permalink: /2012/10/09/ssconvert
post_id: 4822836
categories: 
- gnumeric
- ssconvert
---

Ha egyszerű táblázatkezelőre van szükségem, többnyire 
[gnumeric](http://projects.gnome.org/gnumeric/)-et használok, leginkább azért, mert sokkal gyorsabbnak tűnik a többi hasonló programnál. Bár a táblázatkezelő nem parancssoros program, a mellécsomagolt konverter, az 
[ssconvert](http://projects.gnome.org/gnumeric/doc/sect-files-ssconvert.shtml) igen. Nagyon egyszerűen lehet a különféle táblázatkezelők formátuma között konvertálni. Például egy gnumeric-kel készített fájl így konvertálhatunk excel formátumra:

```
ssconvert konyvek.gnumeric konyvek.xls
```

Ha 
[tömörebben](http://commandline.blog.hu/2010/04/20/bash_zarojeles_kiegeszites) szeretnénk írni:

```
ssconvert konyvek.{gnumeric,xls}
```

Elég sok input és output formátumot ismer:

```
$ ssconvert --list-importers
ID                           | Description
Gnumeric_paradox:paradox     | Paradox database or primary index file (*.db, *.px)
Gnumeric_oleo:oleo           | GNU Oleo (*.oleo)
Gnumeric_xbase:xbase         | Xbase (*.dbf) file format
Gnumeric_psiconv:psiconv     | Psion (*.psisheet)
Gnumeric_QPro:qpro           | Quattro Pro (*.wb1, *.wb2, *.wb3)
Gnumeric_applix:applix       | Applix (*.as)
Gnumeric_Excel:excel         | MS Excel (tm) (*.xls)
Gnumeric_Excel:xlsx          | MS Excel (tm) 2007
Gnumeric_html:html           | HTML (*.html, *.htm)
Gnumeric_sc:sc               | SC/xspread
Gnumeric_XmlIO:sax           | Gnumeric XML (*.gnumeric)
Gnumeric_lotus:lotus         | Lotus 123 (*.wk1, *.wks, *.123)
Gnumeric_plan_perfect:pln    | Plan Perfect Format (PLN) import
Gnumeric_sylk:sylk           | MultiPlan (SYLK)
Gnumeric_OpenCalc:openoffice | Open Document Format (*.sxc, *.ods)
Gnumeric_dif:dif             | Data Interchange Format (*.dif)
Gnumeric_mps:mps             | Linear and integer program (*.mps) file format
Gnumeric_Excel:excel_xml     | MS Excel (tm) 2003 SpreadsheetML
Gnumeric_stf:stf_csvtab      | Comma or tab separated values (CSV/TSV)
Gnumeric_stf:stf_assistant   | Text import (configurable)
$ ssconvert --list-exporters
ID                           | Description
Gnumeric_lpsolve:lpsolve     | LPSolve Linear Program Solver
Gnumeric_html:roff           | TROFF (*.me)
Gnumeric_html:latex_table    | LaTeX 2e (*.tex) table fragment
Gnumeric_html:latex          | LaTeX 2e (*.tex)
Gnumeric_html:xhtml_range    | XHTML range - for export to clipboard
Gnumeric_html:xhtml          | XHTML (*.html)
Gnumeric_html:html40frag     | HTML (*.html) fragment
Gnumeric_html:html40         | HTML 4.0 (*.html)
Gnumeric_html:html32         | HTML 3.2 (*.html)
Gnumeric_Excel:xlsx          | MS Excel (tm) 2007
Gnumeric_Excel:excel_dsf     | MS Excel (tm) 97/2000/XP & 5.0/95
Gnumeric_Excel:excel_biff7   | MS Excel (tm) 5.0/95
Gnumeric_Excel:excel_biff8   | MS Excel (tm) 97/2000/XP
Gnumeric_dif:dif             | Data Interchange Format (*.dif)
Gnumeric_OpenCalc:odf        | ODF/OpenOffice with foreign elements (*.ods)
Gnumeric_OpenCalc:openoffice | ODF/OpenOffice without foreign elements (*.ods)
Gnumeric_GnomeGlossary:po    | Gnome Glossary PO file format
Gnumeric_sylk:sylk           | MultiPlan (SYLK)
Gnumeric_paradox:paradox     | Paradox database (*.db)
Gnumeric_glpk:glpk           | GLPK Linear Program Solver
Gnumeric_stf:stf_csv         | Comma separated values (CSV)
Gnumeric_stf:stf_assistant   | Text (configurable)
Gnumeric_XmlIO:sax           | Gnumeric XML (*.gnumeric)
Gnumeric_pdf:pdf_assistant   | PDF export
```