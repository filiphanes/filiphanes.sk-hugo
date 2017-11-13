+++
date = "2017-11-13T17:17:49+01:00"
tags = [ "video", "streaming", "obs","atem"]
categories = [ "audio-video"]
title = "Priame streamovanie z ATEM Television Studio cez OBS"
description = ""
url = "/audio-video/priame-streamovanie-atem-television-studio-obs"
comments = true
+++
ATEM Television Studio je výborná strižňa za danú cenu. Umožňuje hardvérový enkoding do H.264 kódeku a ukladanie na disk pomocou priloženého softvéru Blackmagic Design Express. Cez Decklink kartu sa da video cez HDMI alebo SDI signál priniesť do počítača a ďalej nahrávať alebo streamovať cez WireCast alebo OBS.

MX Light je super program, ktorý umožňuje aj priamo streamovať z ATEM TVS do rôznych formátov, ale nie je zadarmo a nevie prikladať titulky a púšťať do streamu ďalšie videá.

Ďalší program umožňuje, ktorý je zadarmo vie nahrávať stream z ATEM TVS na disk, ale nevie streamovať.

OBS aj Wirecast dokáže prehrávať Decklink karty, ale ATEM TVS nie..

Kombináciou tohoto programu, VLC a OBS však vieme zabezpečiť streamovanie videa-audia aj s prikldaním titulkov a púšťaním ďalších videí a vôbec softvérovým strihaním.

Otvoríme tento program a klikneme na Preview, ktorý otvorí okno VLC a v ňom sa prehráva video priamo z ATEM strižne bez Deklinku.
V OBS vytvoríme novú vrstvu Window Capture a zvolíme predchvíľou otvorené VLC okno. Toto okno môžeme minimalizovať, ale ak chceme mať najlepšiu kvalitu treba, aby malo video aj okno VLC natívne rozlíšenie a v okne neboli čierne pásy na bokoch, inak bude obraz v OBS buď rozmazaný, alebo zdeformovaný.
A máme v OBS obraz a zvuk z ATEMu a môžeme s ním pracovať ako s akoukoľvek inou vrstvou v OBS. A nakoniec spustiť streamovanie na ktorýkoľvek z podporovaných streamovacích serverov (YouTube, Twitch, ...).

Výhody:

 - všetky výhody strihania a nahrávania ATEMu a OBS
 - netreba kupovať ani zapájať Decklink kartu

Nevýhody:

 - komplikovanejšie spúšťanie
 - možno trochu väčšie nároky na CPU, kvôli dekódovanie a opätovnému enkódovaniu
