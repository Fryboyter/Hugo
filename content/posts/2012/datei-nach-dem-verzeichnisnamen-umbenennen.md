---
title: Datei nach dem Verzeichnisnamen umbenennen
date: 2012-08-12T11:28:00+0100
categories:
- Linux
- OSBN
tags:
- Dateiname
- Verzeichnis
- Umbenennen
slug: datei-nach-dem-verzeichnisnamen-umbenennen
---
Vor kurzem gab es eine Anfrage in einem Forum, wie man eine Datei in einem Verzeichnis unkompliziert umbenennen kann, dass der Dateiname danach dem des Verzeichnisses entspricht. Nehmen wir also mal an, dass die Datei aufnahme1.mkv heißt und das Verzeichnis Mein_bester_Urlaubsfilm.

Mittels des Befehls **find . -name \*.mkv -exec mv '{}' \"${PWD##*\/}.mkv\" \;** wird nach Dateien mit der Endung .mkv gesucht. Wird eine oder mehrere Dateien gefunden, wird nachgesehen wie der Verzeichnisname lautet und die Datei dementsprechend umbenannt. Das klappt natürlich auch mit anderen Dateien. Hierzu einfach das .mkv im Befehl entsprechend der Anforderungen umbenennen.

Mit diesem Befehl wird nun aus aufnahme1.mkv im Verzeichnis Mein_bester_Urlaubsfilm die Datei Mein_bester_Urlaubsfilm.mkv.

Wer eine bessere Lösung hat, kann diese gerne hier angeben.
