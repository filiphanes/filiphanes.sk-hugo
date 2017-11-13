+++
draft = true
date = "2017-11-12T18:55:28+01:00"
title = "Zadarmo blog s hostingom s https a kontaktným formulárom"
description = ""
categories = ["Web-dev"]
tags = ["static","hugo","https","blog"]
url = "/web-dev/zadarmo-blog-hosting-https-kontakty-formular/"
comments = true

+++
V skratke: tento blog je hostovaný zadarmo na netlify.com, s HTTPS a články píšem v Markdowne a generuje sa cez generátor statických stránok hugo takže je aj brutálne rýchly.

Ak vás zaujíma ako som to spravil a ako som sa k tomu dostal, čítajte ďalej.

Keďže som robil webstránky na wordpresse tak som si logicky spravil aj svoju osobnú stránku na ňom.
Potom som hľadal najlacnejší webhosting a neustále zvažoval medzi VPS a webhostingom.
Rozhodol som sa pre najväčší český hosting Wedos a využil ich úvodnú akciu s 50% zľavou takže ma rok hostingu vyšiel na skoro 6 €. Po roku mi však a prišla platba na 12 €.
Spolu s doménou ma by ma teda osobná stránka vychádzala ročne okolo 27 €.

Potom som narazil na github pages, ktoré umožňujú hostovať zadarmo stránku na subdoméne filiphanes.github.io alebo aj na vlastnej doméne. Kód stránky musí byť v github repozitári a ak nechcem platiť, tak musí byť pod opensource licenciou. Github pages neumožňuje SSL. Cez CloudFlare sa však dá rozbehať SSL nad github pages. Toto bolo aj prvotné riešenie, na ktorom som bežal asi 2 týždne. Potom ma znudilo si neustále manuálne u seba kompilovať a nahrávať stránky na github. Na stránge hugo je zoznam hostingov, ktoré podporujú hugo a vybral som si netlify.

Umožňuje:

 - automatickú kompiláciu stránky hneď po nahratí zmien na github repozitár
 - SSL certifikát
 - zbieranie dát z formulárov na stránkach, takže môžem mať formulár na statickej stránke a keď niektorý návštevník vyplní a odošle, príde mi email so všetkými údajmi.
 - upraviť blog z hocikadiaľ, kde mám prístup na github, pretože sa automaticky deployne

Takže nepotrebujem inštalovať Wordpress, zháňať a platiť hostingy s PHP, MySQL alebo riešiť reklamu na freehostingoch alebo riešiť rozbehávanie webservera na VPS. Mám statický blog, ktorý môžem kedykoľvek presunúť kde chcem a upraviť si html témy ako chcem a navyše je rýchly, tak že rýchlejší už ani byť nemôže (možno).

Odkazy:

 - https://gohugo.io/getting-started/usage/
 - https://gohugo.io/hosting-and-deployment/hosting-on-netlify/
 - https://github.com/filiphanes/filiphanes.sk-hugo
