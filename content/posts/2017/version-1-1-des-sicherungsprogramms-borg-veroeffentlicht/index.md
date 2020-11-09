---
title: Version 1.1 des Sicherungsprogramms Borg veröffentlicht
date: 2017-10-09T10:36:52+0100
categories:
- Linux
- OSBN
tags:
- Borg
- Backup
slug: version-1-1-des-sicherungsprogramms-borg-veroeffentlicht
---
Für sogenannte Offside-Backups nutze ich (in der Regel in Verbindung mit rsync.net) das Tool Borg. Borg legt die zu sichernden Dateien in Repositorys an und nutzt zudem auch noch [Deduplikation](https://de.wikipedia.org/wiki/Deduplikation) bei der die Daten in kleine Teile zerlegt werden. Somit werden nur die geänderten Teile bei einer Datensicherung berücksichtigt.

Vor ein paar Tagen wurde nun Borg in Version 1.1 veröffentlicht. Für mich stechen besonders folgende Sachen hervor:

- Borg diff: Vergleichen von zwei Sicherungen
- Borg export tar: Sicherung als Tar-Archiv exportieren
- JSON API für die wichtigsten Sachen wie borg create, borg list usw.
- BORG_PASSCOMMAND: Nutzung von Schlüsselringen und Hardwareschlüsseln wird damit vereinfacht

Da sich bei Borg in Version 1.1 einiges getan hat, gibt es unter [https://www.borgbackup.org/releases/borg-1.1.html](https://www.borgbackup.org/releases/borg-1.1.html) eine Zusammenfassung der wichtigsten Punkte.

Wer sich für Borg für ein Offside-Backup interessiert, sollte sich ggf. einmal den Dienst rsync.net ansehen. Dieser bietet für Nutzer von Attic bzw. Borg einen [Sondertarif](http://rsync.net/products/attic.html)an, bei dem das GB 3 Cent im Monat kostet und man mindestens 25 GB mieten muss. Da ich dort nur meine wirklich, wirklich, wirlich wichtigen Sachen sichere komme ich somit für weniger als 8 Euro im Jahr gut zurecht und habe Dank der Deduplikation noch jede Menge Platz frei. Die Repositorys von Borg lassen sich übrigens verschlüsselt (inkl. Schlüsseldatei) anlegen so dass nur die verschlüsselten Daten hochgeladen werden.
