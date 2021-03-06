---
title: Raspberry Pi Images schrumpfen
date: 2021-03-07T00:00:18+0100
categories:
- Linux
tags:
- Raspberry Pi
- Images
slug: raspberry-pi-images-schrumpfen 
---
Nehmen wir an, man hat einen Raspberry Pi mit einer SD-Karte mit 120 GB komplett eingerichtet und will ein Image erstellen um dies auf andere Raspberry Pi zu installieren. Die meisten Nutzer werden hierfür Befehle wie <mark>dd if=/dev/mmcblk0 of=/home/username/raspberry.img bs=4M</mark> nutzen. Das ist einfach. Hat allerdings einen Nachteil. Die Image-Datei ist 120 GB groß egal wie viel Speicherplatz tatsächlich genutzt wird. Auch wenn Speicherplatz nicht mehr sehr teuer ist verschwendet man diesen in dem Fall. Man müsste das Image also schrumpfen. Was manuell durchaus machbar ist. Oder man nutzt [PiShrink](https://github.com/Drewsif/PiShrink).

Damit lassen sich mittels dd erstellt Image-Dateien auf die tatsächlich genutzte Größe schrumpfen. In meinem Fall hatte ursprünglich 120 GB große Image nur noch eine Größe von 13 GB. Hierfür reicht der einfach Befehl <mark>pishrink.sh rasberry.img</mark> aus.

Erstelle man nun mittels dd den Inhalt des geschrumpften Image auf eine andere SD-Karte und bootet von dieser, passen sich die Partitionen automatisch an die größe der SD-Karte an, so dass der gesamte Speicherplatz zur Verfügung steht. Hierfür baut PiShrink einen entsprechenden Befehl in die Image-Datei ein.
