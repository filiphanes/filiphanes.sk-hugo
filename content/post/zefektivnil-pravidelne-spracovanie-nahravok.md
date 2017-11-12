+++
date = "2016-10-12T21:05:42+01:00"
title = "Ako som zefektívnil pravidelné spracovanie nahrávok"
comments = true
description = ""
categories = ["audio-video"]
tags = ["audio","mp3","encoding","audacity","software"]
url = "audio-video/zefektivnil-pravidelne-spracovanie-nahravok/"

+++
V [kresťanskom spoločenstve](http://milost.sk/) nahrávame 2x týždenne 2 nahrávky – chvály a kázeň.

Nahrávame v mixpulte na USB kľúč. Odtiaľ nahrávku prenášame do notebooku. V [Audacity](http://www.audacityteam.org/) orežeme začiatok, koniec, znormalizujeme hlasitosť a na kázeň aplikujeme aj kompresor. Výsledok uložíme do mp3 formátu a nahráme na google disk, kde si môžu nahrávku vypočuť hodobníci. Pre chvály používame formát mp3 (ABR, najmenej 128kbps kvalitu, [joint stereo](https://sk.wikipedia.org/wiki/Joint_stereo)). Pre kázeň stačí mp3 VBR, 96kbps, mono.

Pri tomto procese je veľa stále rovnakej práce pri kopírovaní wav nahrávky z kľúča a nahrávaní na internet. Preto som použil softvér [GoodSync](http://www.goodsync.com/), ktorý zrýchlil tieto procesy:

- po zasunutí kľúča automaticky skopíruje novú nahrávku na disk.
- túto operáciu je treba spraviť rýchlo, pretože medzi chválami a kázňou nie je veľa času na vyklikávanie a hľadanie správnych priečinkov
- exportovanú mp3 z Audacity automaticky začne nahrávať na google disk.
- chvály a kázeň sa nahrávajú na rôzne google účty a je to veľa času a komplikácií pri prihlasovaní, a navyše v jednom prehliadači byť prihlásený do dvoch účtov a uploadovať je problém.

GoodSync synchronizácia sa dá nastaviť jednosmerne, tak aby nahrávalo iba nové súbory na internet a nesťahovalo milión ďalších na lokálny disk.
Dá sa nastaviť aj to, aby nezačal nahrávať hneď po vytvorení súboru, lebo aj Audacity trvá zopár minút, kým mp3 nahrávku vyexportuje.

