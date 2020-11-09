---
title: Wenn Windows 10 verhindert, dass man NTFS-Partitionen unter Linux mit Schreibrechten mountet
date: 2018-07-07T11:53:00+0100
categories:
- Linux
- OSBN
tags:
- Ntfs-3g
- Windows
- Schnellstart
slug: wenn-windows-10-verhindert-dass-man-ntfs-partitionen-unter-linux-mit-schreibrechten-mountet
---
Auf einenm Rechner ist sowohl Windows als auch Linux installiert. Der Datenaustausch erfolgt über eine NTFS-Partition, die unter Linux mit ntfs-3g eingebunden wird. Seit einiger Zeit wird die Partition aber plötzlich nur noch mit Leserechten gemountet.

Nach einigem hin und her (ftab geprüft, nachgeschaut ob ntfs-3g noch installiert ist usw.) habe ich festgestellt, das Windows die Ursache ist. Bis vor kurzem lief auf dem Rechner noch Windows 7 und wurde nun über das kostenlose Upgrade auf Windows 10 aktualisiert (ja das funktioniert immer noch). Unter Windows 10 gibt es so eine nette Funktion namens [Schnellstart](http://www.soft-management.net/wp/2017/03/der-schnellstart-von-windows-10). Und genau diese Funktion bewirkt, dass ntfs-3g die Partitionen nur mit Leserechten mountet um Probleme zu vermeiden.

Da es bei dem betreffenden Rechner egal ist, ob der Rechner nun in 15 oder 20 Sekunden startet, ist die Lösung recht einfach. Man deaktiviert den Schnellstart. Hierfür öffnet man die Systemsteuerung und wählt unter Hardware und Sound die Energieoptionen aus. Dort gibt es den Punkt "Auswählen, was beim Drücken von Netzschaltern passieren soll". Hier findet man dann unter "Einstellungen für das Herunterfahren" die Option "Schnellstart aktivieren (empfohlen)". Leider ist dieser normalerweise ausgegraut, so dass man hier den Haken nicht entfernen kann. Von daher muss man erst noch auf den Link "Einige Einstellungen sind momentan nicht verfügbar" klicken. Danach kann man den Haken bei "Schnellstart aktivieren (empfohlen)" entfernen und die Einstellungen speichern. Nach einem Neustart von Linux sollte nun die NTFS-Partition wie gewohnt mit Schreibrechten gemountet werden.
