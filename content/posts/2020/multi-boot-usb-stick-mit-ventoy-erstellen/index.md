---
title: Multi-Boot-USB-Stick mit Ventoy erstellen
date: 2020-05-23T12:43:43+0200
categories:
- OSBN
- Linux
tags:
- Ventoy	 
- USB-Stick
- Iso
slug: multi-boot-usb-stick-mit-ventoy-erstellen
---
Der eine oder andere wird sich bestimmt einen USB-Stick erstellt haben mit dem man unterschiedliche Iso-Dateien booten kann. Bei vielen Lösungen ist hierbei einige Handarbeit nötig. Vor ein paar Tagen bin ich auf das Tool [Ventoy](https://www.ventoy.net/en/index.html) gestoßen, das diesen Aufwand sehr minimiert.

Als erstes muss man sich das Tool auf den Rechner installieren (bei Arch Linux ist es im AUR zu finden). Danach steckt man den USB-Stick in einen der USB-Anschlüsse am Rechner und prüft mittels <mark>fdisk -l</mark> wie er ansprechbar ist. Nehmen wir als Beispiel /dev/sdf.

Nun bereitet man mittels <mark>yentoy -i /dev/sdf</mark> (/dev/sdf muss an die eigenen Gegebenheiten angepasst werden) den USB-Stick vor. Ist die Installation abgeschlossen, sollte man auf dem USB-Stick zwei Partitionen haben. Eine kleine für das Booten und die größere für die Iso-Dateien. Abschließend kopiert man die gewünschten Iso-Dateien auf die größere Partition. Und das war es schon. Bootet man nun vom USB-Stick sollte man ein Auswahlmenü erhalten welche der Dateien man starten will. Ich habe es mit der aktuellen Iso-Datei von Arch Linux sowie mit einer Iso-Datei von Windows 10 probiert und es hat problemlos funktioniert.
