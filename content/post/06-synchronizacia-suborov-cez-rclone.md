+++
date = "2019-06-28T20:32:42+01:00"
title = "Synchronizácia súborov cez rclone"
comments = true
description = ""
categories = ["audio-video"]
tags = ["audio","mp3","sharing","rclone","drive"]
url = "audio-video/synchronizacia-suborov-cez-rclone"
image = "img/streaming.jpg"

+++
V [predchádzajúcom článku o spracovaní nahrávok](https://filiphanes.sk/audio-video/zefektivnil-pravidelne-spracovanie-nahravok/)
som písal o synchronizácii súborov na google drive.
Tento systém som odvtedy prerobil, takže teraz môžeme držať celý archív nahrávok na lokálnom serveri
a na google disku držať iba posledný rok, keďže priestor je tam obmedzený.

Celý systém vyzerá nasledovne: lokálny server s 2TB diskom zdieľa cez [sambu](http://www.linuxandubuntu.com/home/what-is-samba-server-and-how-to-setup-samba-server-in-ubuntu-linux/) ostatným počítačom v sieti tento diskový priestor.
Takže, keď z nahrávacieho počítača vytvorí zvukár nahrávku, uloží ju na sieľový disk a okamžite je dostupná pre ostatné počítače. Napríklad video počítač, kde bude treba túto nahrávku pridať do videa.

Na serveri bežia crony, ktoré pravidelne synchronizujú priečinok s nahrávkami na google disk. Tieto crony spúšťajú nástroj [rclone](https://rclone.org/drive/). Zatiaľ rclone neposkytuje obojsmernú synchronizáciu ako goodsync, takže, aby som predišiel premazávaniu súborov nahratých cez webové rozhranie google disku, synchronizácia prebieha príkazom [rclone copy](https://rclone.org/commands/rclone_copy/) a [rclone sync](https://rclone.org/commands/rclone_sync/). Takto sa nestane, že by sa súbor automaticky premazal.

    # Najprv sa spúšťa
    rclone sync /mnt/disk/moj@gmail.com/audio remote:/audio
    # a potom
    rclone copy remote:/audio /mnt/disk/moj@gmail.com/audio

Takto vyzerá crontab:

    # crontab -e
    # zalohovanie z cloudu na lokalny disk
    0 8 * * 0 rclone copy nahravky:/ /mnt/disk/moj@gmail.com/ --no-update-modtime --drive-skip-gdocs >> /var/log/rclone/nahravky.log
    # nahratie novych suborov na cloud
    */5 14 * * 0 rclone sync /mnt/disk/moj@gmail.com/audio/ nahravky:/audio/ --no-update-modtime --drive-skip-gdocs >> /var/log/rclone/nahravky.log

Taktýmto spôsobom cez rclone je možné synchronizovať aj viaceré priečinky do rôznych google účtov z jedného počítača, čo nie je možné cez klasický google disk client.

