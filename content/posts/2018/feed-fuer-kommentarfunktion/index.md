---
title: Feed für Kommentarfunktion
date: 2018-09-17T19:30:00+0100
categories:
- OSBN
- Allgemein
tags:
- Isso
- Feed
- Kommentarfunktion
slug: feed-fuer-kommentarfunktion
---
Da Bolt CMS keine Kommentarfunktion anbietet nutze ich hierfür Isso. In der aktuellen offiziellen Version gibt es leider keine Möglichkeit, dass man über neue Kommentare informiert wird (was den einen oder anderen Nutzer nervt (inkl. mir selbst)). In der aktuellen Entwicklerversion ist zwar ein Kommentar-Feed vorhanden, allerdings bekomme ich diese auf Uberspace 7 nicht zum laufen.

Ich habe mir daher, bis eine neue Version von Isso auf PyPi veröffentlicht wird, eine Übergangslösung gebaut. Ab sofort findet man unter der Kommentarfunktion einen Link über den man den RSS-Feed für die Kommentare abonieren kann. Dieser ist nicht auf den jeweiligen Artikel beschränkt sondern berücksichtigt Kommentare aller Artikel. Da hier nicht täglich unzählige Kommentare abgegeben werden, dürfte das kein Problem sein. Zudem habe ich den Feed auf die letzten 20 Einträge beschränkt. Der Cronjob der das Script zum Erzeugen der XML-Datei ausführt läuft alle 15 Minuten. Somit werden neue Kommentare im Feed etwas verzögert angezeigt. Dies gilt allerdings nur für die Kommentare die ich freigeschaltet habe.

Wer noch Fehler findet, kann sich gerne melden. Das Problem mit der Formatierung der Kommentare im Feed ist bekannt, allerdings fällt mir hierzu aktuell keine Lösung ein. Zum Benachrichtigen über neue Kommentaresollte es aber trotzdem gut genug sein.