+++
date = "2019-07-07T21:30:00+02:00"
title = "Zdielanie LTE internetu na lokálnej sieti"
comments = true
description = ""
categories = ["audio-video"]
tags = ["lte", "networking","iptables","mikrotik","ubuntu"]
url = "audio-video/zdielanie-lte-internetu-na-lokalnej-sieti/"
image = "img/streaming.jpg"

+++
Telekom DSL internet s rýchlosťou 10/1 je v tejto dobe naozaj pomalý.
Na vysielanie live video je bez debaty nevhodný. V našej lokalite sa nenašiel
lokálny poskytovateľ, ktorý by vedel po kábli alebo optike doviesť dostatočne
rýchly internet. Preto sme sa rozhodli pre mobilný internet od 4ky
za 12€/mesiac s rýchlosťou v lokalite Martin-centrum okolo 20/20Mbit.
Kúpili sme LTE USB modem za 50€ a pripojili do počítača a všetko fungovalo.

Lenže internet je treba pre viaceré počítače v lokálnej sieti. Najprv som
chcel zapojiť USB modem do Mikrotik Routeru, ktorý vraj podporuje aj
USB modemy na prístup do internetu. Toto riešenie sa mi však nepodarilo
rozbehať. Asi nebol modem kompatibilný s routerom alebo som sa dostatočne
nezavŕtal do nízkoúrovňovej komunikácie medzi routerom a modemom
(AT príkazy apod.)

Plán B bol nechať zapojený USB modem do lokálneho servera a zdieľať internet
z neho cez router do ostatných počítačov. Táto možnosť sa ukázala funkčná.
Bolo treba na serverovom ubuntu nakonfigurovať modem cez príkazový riadok
a cez iptables vyzdieľať internet na lokálnu sieť.

Iptables nastavenia:

    #!/bin/bash
    sudo iptables -A FORWARD -o usbltemodem -i eth0 -m conntrack --ctstate NEW -j ACCEPT
    sudo iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
    sudo iptables -t nat -F POSTROUTING
    sudo iptables -t nat -A POSTROUTING -o usbltemodem -j MASQUERADE

Na routeri bolo treba presmerovať všetku internetovú komunikáciu na lokálny
server. Nakoniec sa to podarilo.
