---
title: Mandriva ist tot. Lang lebe Arch Linux und Mandriva in der Box
date: 2010-05-24T19:08:00+0100
categories:
- Linux
- OSBN
tags:
- Mandriva
- Mandrake
- Arch
- Linux
slug: mandriva-ist-tot-lang-lebe-arch-linux-und-mandriva-in-der-box
---
Ich habe Köpfe mit Nägeln gemacht. Oder so ähnlich.

Seit Version 7.x lief hier eigentlich als Produktivsystem immer Mandriva (ehemals Mandrake). Nun nicht mehr. Ich bin nun wirklich ins Arch-Lager gewechselt. Warum genau kann ich eigentlich nicht sagen. Ich würde mal sagen wegen dem Spieltrieb. Wie lange ich es durchhalte? Gute Frage. Um nicht zu sehr unter den Entzugserscheinungen zu leiden, läuft eine Mandriva-Installation unter VirtualBox weiter. Ganz ohne geht es halt doch nicht.

Die Installation ging, wie auch unter VirtualBox, recht schmerzfrei von statten. Nur der Drucker hat mich Nerven gekostet. Naja eher Cups, das in der aktuellen Version scheinbar so seine Probleme mit USB-Druckern hat. Einzig und alleine mein Homebankingprogramm Moneyplex habe ich bisher noch nicht zum laufen bekommen. Egal was ich mache, ich bekomme immer die Fehlermeldung **/home/holycore/moneyplex/moneyplex: symbol lookup error: /home/mathmos/moneyplex/moneyplex: undefined symbol: initPAnsiString**. Sollte jemand die Lösung kennen, bitte melden. Das was man mit Google findet hat nicht wirklich geholfen. Da muss die Tage vermutlich mal der Support von Moneyplex herhalten. Zwischenzeitlich läuft es eben über die Mandriva-Installation unter VirtualBox.

Nachtrag am 24.05.10:

Scheinbar bin ich dann doch nicht so blöd wie ich aussehe. Ich habe mich heute nochmals dem Problem mit Moneyplex gewidmet. Und was soll ich sagen? Es läuft wieder. Wenn man es genau nimmt war ich mal wieder das Problem. Ich hatte bei meinem ersten Versuch das Paket libjpeg6 6b-9 aus AUR installiert. Das mag Moneyplex scheinbar nicht. Das Paket lib32-libjpeg6 6b-1 aus AUR hat dann Moneyplex auf die Sprünge geholfen.
