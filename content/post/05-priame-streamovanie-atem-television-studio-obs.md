+++
date = "2017-11-13T17:17:49+01:00"
tags = [ "video", "streaming", "obs","atem","youtube"]
categories = [ "audio-video"]
title = "Priame streamovanie z ATEM Television Studio cez OBS"
description = ""
image = "img/streaming.jpg"
url = "/audio-video/priame-streamovanie-atem-television-studio-obs"
comments = true

+++
[ATEM Television Studio](https://www.blackmagicdesign.com/products/atemtelevisionstudiohd) je výborná strižňa za danú cenu. Staršia aj nová verzia. Umožňuje hardvérový encoding do H.264 kódeku a ukladanie na disk pomocou priloženého softvéru [Media Express](https://www.blackmagicdesign.com/products/decklink/mediaexpress). Cez [Decklink kartu](https://www.blackmagicdesign.com/products/decklink) sa dá video cez HDMI alebo SDI signál priniesť do počítača a ďalej nahrávať alebo streamovať cez WireCast alebo OBS.

{{< figure src="/img/atemtelevisionstudio.jpg" title="ATEM Television Studio" >}}

[MX Light](http://mxlight.co.uk) je tiež super program, ktorý umožňuje priamo streamovať z ATEM TVS do rôznych formátov, ale nie je zadarmo a nevie prikladať titulky a púšťať do streamu ďalšie videá ako [OBS](https://obsproject.com).

[MXPTiny](https://ianmorrish.wordpress.com/tag/mxptiny/), ktorý je zadarmo vie nahrávať stream z ATEM TVS na disk, ale nevie streamovať.

[OBS](https://obsproject.com) aj [Wirecast](https://www.telestream.net/wirecast/overview.htm) dokáže prehrávať vstup z Decklink karty, ale ani jeden nedokáže naberať video z ATEM TVS.

Kombináciou MXPTiny, [VLC](https://www.videolan.org) a [OBS](https://obsproject.com) však vieme zabezpečiť streamovanie videa/audia aj s prikladaním titulkov, lowerthirds  a púšťaním ďalších videí a vôbec softvérovým strihaním.

Otvoríme MXPTiny a klikneme na Preview, ktorý otvorí okno VLC a v ňom sa prehráva video priamo z ATEM TVS strižne bez Decklinku.
V OBS vytvoríme novú vrstvu [Window Capture](https://jp9000.github.io/OBS/sources/windowcapture.html) a zvolíme predchvíľou otvorené VLC okno. Toto okno môžeme minimalizovať, ale ak chceme mať najlepšiu kvalitu, treba mať okno VLC s natívnym rozlíšením a aby v okne neboli čierne pásy na bokoch, inak bude obraz v OBS buď rozmazaný, alebo zdeformovaný.
A máme v OBS obraz a zvuk z ATEMu a môžeme s ním pracovať ako s akoukoľvek inou vrstvou v OBS. A nakoniec stačí spustiť streamovanie na ktorýkoľvek z podporovaných streamovacích serverov ([YouTube](https://www.youtube.com/channel/UC4R8DWoMoI7CAwX8_LjQHig), [Twitch](https://go.twitch.tv), ...).

Výhody:

 - všetky výhody strihania a nahrávania v ATEMe a OBS
 - netreba kupovať ani zapájať Decklink kartu ani zapájať ďalší kábel https://syntex.sk/sk/strihove-karty/blackmagic-design-decklink-mini-recorder-9338716001921.html

Nevýhody:

 - komplikovanejšie spúšťanie
 - možno trochu väčšie nároky na CPU, kvôli dekódovanie a opätovnému enkódovaniu, ale zatiaľ som nepostrehol na i5 CPU žiadne problémy ani pri rozlíšení 1080i50

Odkazy:

 - https://github.com/baycom/MXPTiny
 - https://ianmorrish.wordpress.com/tag/mxptiny/
 - http://ml.42u.de/download/MXPTinyinstall.exe
