---
title: KDE Plasma und Claws-Mail stürzen beim Herunterfahren oder bei einem Neustart ab
date: 2015-05-20T08:46:00+0100
categories:
- Linux
- OSBN
tags:
- KDE
- Plasma
- Claws Mail
- Absturz
slug: kde-plasma-und-claws-mail-stuerzen-beim-herunterfahren-oder-bei-einem-neustart-ab
---
Ausgangssituation ist folgende. Auf einem Rechner läuft Arch Linux mit KDE Plasma. Updates sind zum aktuellen Stand komplett eingespielt. Egal ob der Rechner herunter gefahren oder neu gestartet wird, es stürzt die Plasmashell sowie das durchgehend laufende Programm Claws-Mail mit einem Signal 11 ab. Nachdem man einige Fenster mit den Absturzmeldungen weg geklickt hat, startet der Rechner dann aber wie beabsichtigt neu oder fährt komplett herunter. Besonders wohl ist mir dabei aber nicht wegen Claws-Mail.

Nach einigem hin und her habe ich gestern die Lösung gefunden. Der verdammte Layer 8 war mal wieder das Problem... Vor einiger Zeit gab es eine Änderung mit der der Microcode eines Intel-Prozessors nicht mehr automatisch aktualisiert wird und somit ein [Eingreifen des Nutzers](https://www.archlinux.org/news/changes-to-intel-microcodeupdates "Eingreifen des Nutzers") nötig ist. Vor einigen Wochen hatte ich mir die Datei /boot/syslinux/syslinux.conf verbastelt, so dass ich die vorhandene gelöscht und eine neue erstellt habe. Dabei habe ich natürlich nicht den Eintrag für das Update des Microcodes eingebaut... Nachdem ich das jetzt nachgeholt habe, funktioniert alles wieder wie es soll. Warum das ganze aber erst nach Wochen Probleme gemacht hat, kann ich nicht wirklich sagen. Scheinbar gab es ein Update, dass mit einer alten Version Probleme hat.
