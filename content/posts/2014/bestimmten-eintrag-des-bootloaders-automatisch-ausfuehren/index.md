---
title: Bestimmten Eintrag des Bootloaders automatisch ausführen
date: 2014-01-20T13:32:00+0100
categories:
- Linux
- OSBN
tags:
- Bootloader
- Neustart
- Extlinux
- Rebootin
slug: bestimmten-eintrag-des-bootloaders-automatisch-ausfuehren
---
Wer von euch ein Dualbootsystem nutzt wird das Problem bestimmt kennen. Man arbeitet unter Linux und braucht dann z. B. zur Entspannung, oder weil es ein bestimmtes Programm nicht unter Linux gibt, Windows. Normalerweise startet man dann den Rechner neu, wartet bis der Bootloader soweit ist, wählt den Eintrag für Windows und wartet dann wieder, bis Windows gestartet ist. Gerade der Teil bei dem man auswählt, was der Bootloader starten soll, nervt hier dann doch. Unter Mandrake bzw. Mandriva hatte ich hierzu immer [rebootin](/rebootin/ "rebootin") genutzt. Damit konnte man unter Linux im laufendem Betrieb angeben, welcher Eintrag des Bootloaders Grub nach einem Neustart (welcher automatisch ausgeführt wird) genutzt werden soll. Unter Arch vermisse ich das kleine Tool. Davon abgesehen nutze ich inzwischen syslinux als Bootloader. Damit kann rebootin meines Wissens nach nichts anfangen.

Gestern habe ich mich mal wieder wegen einer anderen Sache mit syslinux beschäftigt. Dabei bin ich auf extlinux gestoßen. Dieses Tool ist im Paket von syslinux enthalten. Zumindest unter Arch Linux. Und was muss ich sehen? Das ist, unter anderem, ein Ersatz für rebootin.

Mittels dem Befehlen **extlinux --once=windows /boot/syslinux** und einem anschließendem **reboot** wird Linux heruntergefahren, der Rechner neu gestartet der gewünschte Eintrag im Bootloader gestartet. Die Einträge für das Bootmenü bei Syslinux werden über sogenannte Labels definiert. Anstelle von windows wie im genannten Beispiel, nimmt man einfach das Label des Eintrags, den man ausführen will. Anstelle von --once können die Schreibfaulen auch einfach -o nehmen. Sollte syslinux an einer anderen Stelle als /boot/syslinux liegen, muss man dies auch noch anpassen. Spontan fällt mir aber kein Grund ein, wieso das so sein sollte. Packt man den Spass dann noch in ein Script und verpasst dem normalen Nutzer die nötigen Rechte, hat man quasi eine recht bequeme Möglichkeit in ein anderes Betriebssystem zu booten. Mal sehen, ob ich das ganze noch in das Startmenu AppMenu QML packen kann, welches bei mir zum [Einsatz](/appmenu-qml-mein-neues-startmenue-und-dessen-problembeseitigung/ "AppMenu QML") kommt.
