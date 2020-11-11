---
title: Warum man immer erst die SuFu nutzen sollte
date: 2013-08-15T09:30:00+0100
categories:
- Linux
- OSBN
tags:
- Suchfunktion
- Layer 8
slug: warum-man-immer-erst-die-sufu-nutzen-sollte
---
Gestern hatte ich mal wieder ein Erlebnis, bei dem man sich nur an den Kopf fassen konnte. Diesmal allerdings wegen eigener Dummheit. Als ich gestern mein Netbook mal wieder mit den neuen Updates von Arch-Linux versorgen wollte, ist während der Installation ist irgendwann der Rechner ausgegangen. Wann genau kann ich nicht sagen, da ich nicht die ganze Zeit vorm Rechner war. Aber die Ursache war auf jeden Fall ein leerer Akku.

Tja, man sollte wirklich erst mal den Akkustand prüfen, bevor man die Updates einspielt. Das habe ich dann nachdem ich das Netzkabel angeschlossen und die Kiste wieder gestartet habe feststellen müssen. Kurz nachdem ich unter LXDE angemeldet habe, gab es eine nette Kernel Panic.

Also wieder ein Neustart. Danach ganz schnell angemeldet und versucht die Logs unter /var/log anzusehen. Kernel Panic. Nächster Versuch. Diesmal allerdings kein Versuch Logs anzusehen, sondern pacman -Syu aufgerufen. Eventuell wurde wegen des leeren Akkus ja nur ein Paket nicht ganz installiert. Kernel Panic. Hmm... Eventuell hat das Dateisystem eine Macke? Also gut, dann booten wir eben die Kiste mal mit dem Installationsmedium von Arch und prüfen mal das Dateisystem der Root- und Homepartion. Hier gab es mal keine Kernel Panic, sondern erst mal eine Hürde, wie man mittels Luks verschlüsselte LVM mountet. Also schnell mal mit dem Smartphone gegoogelt. Ach so geht das... Ein Check des Dateisystems ergab aber nichts. Nicht mal eine Kernel Panic. Also gut, dann schauen wir mal die Logs an. Nichts.

Das suchen wir den Fehler Spielchen habe ich dann noch ca. 2 Stunden gespielt und mich dann entschieden, die persönlichen Daten am Wochenende zu sichern und die Kiste neu zu installieren. Das geht auf jeden Fall schneller. Gut, dass ich aber noch am gleichen Abend im Forum von archlinux.org vorbeigeschaut habe. Dort habe ich dann [diesen](https://bbs.archlinux.org/viewtopic.php?id=168177 "Kernel Panic Broadcom") Thread gefunden. Und genau in dem Moment habe ich mir an den Kopf gefasst. Denn mein Netbook hat einen Broadcom-Chip für das WLAN, welcher das Modul brcmsmac nutzt. Und bei der abgebrochenen Aktualisierung war bei den neuen Paketen auch der Kernel Linux 3.10.6 dabei. Scheinbar lief die Aktualisierung wohl doch durch. Zumindest bis zum Kernel.

Ich habe mich daher erst mal entschlossen, wieder den alten Kernel 3.10.5 zu installieren. Und schon läuft die Kiste wieder. Da Broadcom ja nicht gerade der Hit unter Linux ist, überlege ich mir jetzt allerdings noch, ob die die WLAN-Karte gegen eine andere z. B. von Intel tausche. Allerdings soll Lenovo ja im Bios eine Whitelist führen und so viele Karten aussperren.
