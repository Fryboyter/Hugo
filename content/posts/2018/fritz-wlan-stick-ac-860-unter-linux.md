---
title: Fritz!WLAN Stick AC 860 unter Linux
date: 2018-12-19T19:38:00+0100
categories:
- Linux
- OSBN
tags:
- Fritz
- Wlan
- AC 860
slug: fritz-wlan-stick-ac-860-unter-linux
---
In meinem Notebook ist eine Centrino Advanced-N 6205 WLAN-Karte verbaut. Diese verbindet, egal was ich mache, mit maximal 54 MB/s (genutzt wird noch weniger). Laut Google bin ich wohl nicht der einzige mit dem Problem. Also muss etwas her das mehr Bandbreite bietet.

Normalerweise würde ich einfach die Karte wechseln. Was bei Geräten von Lenovo (zumindest bei älteren Modellen) nicht ganz so einfach ist. Denn im Bios / UEFI ist eine Whitelist vorhanden. Somit funktionieren nur bestimmte Karten. Eine offizielle Aufstellung funktionierender Karten gibt es natürlich nicht. Weihnachtsgeld sei dank habe ich mir spontan den WLAN-USB-Stick AC 860 von AVM gekauft.

Im Lieferumfang findet man neben dem USB-Stick auch einen USB-Standfuß sowie eine Anleitung.

Auf dem Notebook ist Arch (Kernel 4.19.9) installiert. Gleich nach dem anschließen des Sticks wird dieser erkannt und startet im sogenannten CD-ROM-Modus. Auf diesem "CD-ROM" sind die Treiber gespeichert. Natürlich für Windows. Das ist zum einen für Linux überflüssig und zum anderen bleibt der Stick in diesem Modus hängen. Super.

Die Lösung ist allerdings ziemlich einfach. Man muss einfach usb_modeswitch installieren. Bei Arch liegt das Paket in den community Paketquellen. Stöpselt man dann den Stick an, startet er im richtigen Modus durch.

Für die Netzwerkverbindungen auf meinem Notebook verwende ich netctl. Hier musste ich nur die Bezeichnung des alten Interface gegen die des neuen in der Konfigurationsdatei austauschen. Und schon steht die Verbindung. Theoretisch sind laut Router 866 / 866 Mbit/s möglich. In der Praxis ist der Stick mit 650 / 780 Mbit/s verbunden und läuft stabil. Mal schauen ob man hier noch etwas an der einen oder anderen Schraube drehen kann. Alles in allem bin ich zufrieden. Endlich kann ich die komplette Bandbreite meines Internetanschlusses auch mit dem Notebook ausreizen. Einen Datentransfer im LAN konnte ich noch nicht testen. Ich gehe aber davon aus, dass das auch keine Probleme macht.

Noch ein Hinweis zum Schluss. Der Stick wird erst ab Kernel 4.19 unterstützt.
