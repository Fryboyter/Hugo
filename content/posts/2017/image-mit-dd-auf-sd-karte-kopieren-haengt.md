---
title: Image mit dd auf SD-Karte kopieren hängt
date: 2017-11-11T15:40:20+0100
categories:
- Linux
- OSBN
tags:
- Image
- Dd
- Oflag
slug: image-mit-dd-auf-sd-karte-kopieren-haengt
---
Da ich Ende des Jahres für ein paar Monate einen Server mit CentOS übernehme, wollte ich mir mal eben CentOS auf eine SD-Karte für einen Raspberry installieren. Mal eben...

Das Wiki von CentOS gibt in der Installationsanleitung "dd if=CentOS-Userland-7-armv7hl-Minimal-RaspberryPi3.img of=/dev/mmcblk0 bs=8192; sync" an. Dieser Befehl hängt bei mir allerdings für mehrere Stunden. Kann eigentlich nicht sein. Htop zeigt bei dem Prozess den Status D an. Nach etwas Google-Fu habe ich herausgefunden, dass dies für "uninterruptible sleep (usually IO)" steht. Solche Prozesse lassen sich nicht mal mit Rootrechten killen.

Also nächster Versuch bei dem bei obigen Befehl den Teil mit dd um status=progress erweitert habe. Hier werden laut Anzeige die 3 GB der Images ratz fatz bearbeitet. Und dann bleibt das ganze wieder stundenlang hängen. Bei den nächsten Versuchen habe ich etwas mit bs=8192 gespielt und die Werte geändert. Und wieder kein Erfolg.

Etwas Google-Fu später habe ich den Tipp gefunden, die Daten nicht zu cachen sondern direkt zu schreiben. Hierzu erweitert man den Teil mit dd einfach um oflag=direct. Das ist dann zwar langsamer, führt aber bei mir zumindest zum Erfolg.

Die Karte ist laut badblocks übrigens in Ordnung. Das habe ich zwischenzeitlich auch schon getestet. Die Karte verrichtet ja schon ein paar Jahre ihren Dienst in einem Rapsberry Pi. Jetzt muss ich nur noch herausfinden, wieso es mit Cache so lange dauert. Vor allem weil es sich um eine Karte der Klasse 10 handelt.
