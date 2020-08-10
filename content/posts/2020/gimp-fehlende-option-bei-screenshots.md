---
title: Gimp - fehlende Option bei Screenshots
date: 2020-08-10T18:00:21+0200
categories:
- OSBN
- Linux
tags:
- Gimp  
- Plasma
- DBus
slug: gimp-fehlende-option-bei-screenshots
---
Wie vielleicht dem einen oder anderen bekannt ist, kann man mit dem Programm [Gimp](https://www.gimp.org/) auch direkt Screenshots erstellen. Hierzu wählt man im Menü "Datei" -> "Erstellen" -> "Bildschirmfoto..." aus. Dort sollte man eigentlich auch die Auswahlmöglichkeit habe einen bestimmten Bereich des Bildschirms auzuwählen.

<img alt="Gimp" src="/files/gimp_dbus.png">

Unter KDE Plasma erscheint aber diese Option nicht. Die Lösung ist allerdings ziemlich einfach. Wenn man Gimp mittels dbus-lauch startet (z. B. <mark>dbus-launch gimp %U</mark>) startet, dann erscheint die gewünschte Option.

Bekannt ist das Problem scheinbar schon länger. Zumindest gibt es einige Bugmeldungen bei diversen Distributionen. Warum das Problem bei Gimp oder Plasma bisher nicht behoben wurde, kann ich nicht sagen.
