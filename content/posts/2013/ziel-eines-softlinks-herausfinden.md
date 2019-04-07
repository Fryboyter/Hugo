---
title: Ziel eines Softlinks herausfinden
date: 2013-04-01T17:38:00+0100
categories:
- Linux
- OSBN
tags:
- Ziel
- Softlink
slug: ziel-eines-softlinks-herausfinden
---
Gerade war ich per SSH mit einem anderen Rechner verbunden. Hier hatte ich vor einiger Zeit einen Softlink erstellt. Da dieser nicht mehr funktioniert, hat sich scheinbar das Ziel geändert. Leider hatte ich keinen blassen Schimmer mehr, wohin der Softlink zeigt. Ja, nicht vorhandene Dokumentationen sind schon etwas feines... Um zukünftig nicht wieder ewig nach der Lösung zu suchen, hier selbige für mich und euch. Es gibt den Befehl readlink. Mit diesem kann man sich anzeigen lassen, wohin der Softlink gelenkt wird.

>readlink www.fryboyter.de

Dies gibt z. B. html/cms aus. Will man es etwas genauer haben, kann man den Befehl wie folgt erweitern

>readlink -f www.fryboyter.de

Nun erhält man beispielsweise /var/www/virtual/anaximander/html/cms als Ausgabe.
