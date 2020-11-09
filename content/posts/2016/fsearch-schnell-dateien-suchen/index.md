---
title: FSearch - Schnell Dateien suchen
date: 2016-12-28T22:37:00+0100
categories:
- Linux
- OSBN
tags:
- Dateien
- Suchen
- Fsearch
slug: fsearch-schnell-dateien-suchen
---
Dem einen oder anderen Windowsnutzer wird Everything ein Begriff sein. Mit diesem Tool lassen sich sehr schnell Dateien finden. Everything nutzt hierzu die Metadaten des Master File Table von NTFS. Und was ist mit Linux?

Lösungen wie Baloo habe ich immer links liegen lassen, da mir die Indexierung zu lange dauert und zu viele Resourcen verbraten werden. Daher habe ich bisher immer auf die langsameren Lösungen wie find zurückgegriffen. Heute wurde ich auf [FSearch](https://github.com/cboxdoerfer/fsearch) aufmerksam. Hierbei handelt es sich um ein GTK+3-Programm, welches aktuell noch Alpha-Status hat. Der Entwickler will mit FSearch eine Linux-Alternative zu Everything schaffen.

Und was soll ich sagen? Bisher bin ich schwer begeistert. Nach dem ersten Start gibt man die Verzeichnisse an, welche bei der Suche berücksichtigt werden sollen. Bei meinem ersten Test habe ich das Homeverzeichnis meines Notebooks angeben. Eigentlich habe ich erwartet, dass das Programm eine gewisse Zeit arbeiten wird. Hat es aber nicht. Innerhalb einer Sekunde (geschätzt) wurde mir angezeigt, dass 56153 Einträge bei der Suche berücksichtigt werden. Eine richtige Indexierung war das wohl nicht. Trotzdem hat es mich interessiert wie schnell eine Datei gefunden wird. Auf dem Rechner liegen einige Dateien deren Namen ich auswendig kenne in einem ziemlich verschachtelten Verzeichnisbaum. Das ideale Ziel. Ich habe hier bewusst nur einen Teil des Namen bei der Suche angegeben (also beispielsweise wenn der Dateiname HundKatzeMaus.sql lautet habe ich nach Katze gesucht). Da das Tool bereits beim Tippen anfängt zu suchen wurden mir die Treffer quasi sofort angezeigt. Ich will mich jetzt nicht zu weit aus dem Fenster lehnen aber FSearch fühlt sich sogar schneller als Everything an. Holy Cow.

Die Suche funktioniert zudem auch mittels Wildcards und RegEx und sollte daher eigentlich alle Fälle abdecken. Leider gibt es, zumindest derzeit, keine Version für die Komandozeile. Aber auf Rechnern mit grafischer Oberfläche werde ich FSearch sicherlich öfters nutzen.
