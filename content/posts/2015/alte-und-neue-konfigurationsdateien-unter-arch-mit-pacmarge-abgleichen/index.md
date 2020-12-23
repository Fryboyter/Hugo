---
title: Alte und neue Konfigurationsdateien unter Arch mit pacmarge abgleichen
date: 2015-11-28T13:57:00+0100
categories:
- Linux
- OSBN
tags:
- Arch Linux
- Konfigurationsdateien
- Abgleichen
slug: alte-und-neue-konfigurationsdateien-unter-arch-mit-pacmarge-abgleichen
---
Bei einem Update von Arch Linux kann es passieren, dass es auch Änderungen an den Konfigurationsdateien gibt. Anstelle dass bereits vorhandene Konfigurationsdateien automatisch angepasst oder sogar komplett überschrieben werden, werden die neuen Konfigurationsdateien mit der Endung .pacnew angelegt. Somit ist es dann die Aufgabe des Administrators die vorhandenen Konfigurationsdateien mit den Pacnew-Dateien abzugleichen. Für diesen Job nutze ich ein [Script](/pacnew-dateien-verwalten/), welches sowohl vorhandene als auch Pacnew-Dateien aufspürt und beide mit meld öffnet, so dass ich diese händisch abgleichen kann.

Der Arch-Entwickler foutrelis hat hierfür nun das Tool [pacmarge](https://github.com/foutrelis/pacmarge "pacmarge") gebaut, welches diese Aufgabe automatisiert. Man findet es im AUR. Führt man pacmarge nach einem Update aus, welches auch die Konfigurationsdateien betrifft, erhält man beispielsweise folgende Ausgabe.

{{< image src="pacmarge.png" alt="pacmarge" >}}

Hier sieht man dass bis auf die Datei mirrorlist alle Dateien erfolgreich zusammengeführt wurden. Aber vertrauen ist gut, Kontrolle ist besser. Von daher habe ich die vorhandenen Konfigurationsdateien bereits vorab gesichert und dann mit den durch pacmarge geänderten Dateien verglichen. So wie es aussieht macht das Tool seine Arbeit wirklich gut. Einen Fehler konnte ich nicht finden. Dennoch werde ich wohl bei meinem Script und meld bleiben. Wenn da etwas schief geht, kenne ich die Fehlerquelle definitiv. Layer 8.
