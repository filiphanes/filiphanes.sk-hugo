+++
date = "2019-06-30T21:30:00+02:00"
title = "OpenLP video background"
comments = true
description = ""
categories = ["audio-video"]
tags = ["openlp", "obs", "video"]
url = "audio-video/openlp-video-background/"
image = "img/streaming.jpg"

+++
Na zobrazovanie textov piesní používame [OpenLP](https://openlp.org/) program, ktorý má však už niekoľko verzií problém prekrývať video pozadie prehrávané cez VLC pod ním. Najnovšie riešenie si pomohlo programom [OBS Studio](https://obsproject.com/), ktorý už používame na nahrávanie a live streaming.

OpenLP poskytuje cez remote plugin zobrazovanie výstupu v html prehliadači cez adresu http://localhost:4316. Poskytuje 2 typy výstupu:
1. stage view pre spevákov zobrazuje aj nasledujúce verše
2. pre normálny výstup

Ten druhý typ výstupu som pridal nastavil v OBS do vrstvy Prehliadač s priehľadným pozadím. Podmienkou je, aby aj motív v openlp mal priehľadné pozadie.
Pod ňou je vrstva s video pozadím nastavená do slučky. Takýchto vrstiev môže byť v OBS pripravených viac a človek si potom môže prepínať pozadia v OBS.
Výstup OBS je nastavený na projektorový výstup a výstup OpenLP je nastavený na oblasť úplne mimo (napr. start x=2000,y=2000) aby neprekrýval výstup z OBS.

Ak ste používali na skrývanie titulkov klávesovú skratku D, teraz treba používať T, aby bolo stále vidno video pozadie.

Toto riešenie funguje spoľahlivo aj pre menej technicky zdatných ľudí. Iba prvotné nastavenie si vyžaduje viac technických znalostí. Potom stačí spustiť dva programy a všetko funguje, keďže OpenLP aj OBS si pamätajú nastavenia.
