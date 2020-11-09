---
title: Wordpress ist in Rente gegangen
date: 2017-06-26T17:54:43+0100
categories:
- OSBN
- Allgemein
tags:
- Fryboyter
- Wordpress
- Bolt CMS
slug: wordpress-ist-in-rente-gegangen
---
Heute habe ich Fryboyter.de auf Bolt CMS umgestellt. Das Theme ist, wie man unschwer erkennen kann, Marke Eigenbau. Nach X Versionen mit Schnick Schnack habe ich es einfach mit Fokus auf den Text gehalten.

Für mich ist die Seite aber weiterhin "Beta", da noch einige Sachen nicht so sind, wie ich es gerne haben möchte.

Wenn man aktuell einen Artikel aufruft erscheint an dessen Ende eine Liste mit Artikel-Vorschlägen. Diese sind aktuell noch unabhängig von der Kategorie. Hier möchte ich es noch schaffen, dass nur Artikel der gleichen Kategorie(n) angezeigt werden den dem aufgerufenen Artikel zugeordnet sind.

Den OSBN-Feed erzeuge ich derzeit alle 30 Minuten über eine PHP-Datei, da sich die Feed-Erweiterung von Bolt CMS nur auf Inhaltstypen und nicht auf Kategorien einschränken lässt. Hier will ich mittelfristig auf eine andere Lösung finden, da die Datei auch dann erzeugt wird, wenn kein neuer Artikel vorhanden ist. Erreichbar ist der Feed nun über https://fryboyter.de/files/feed.xml. Die alte Adresse des OSBN-Feed wird per .htaccess umgeleitet, so dass hier keine Probleme entstehen sollten (sofern der Feed-Reader die Umleitung kapiert).

Die Kommentare laufen ab sofort über [Isso](https://posativ.org/isso). Die Daten werden hierbei in einer SQLite-Datenbank auf meinem Webspace gespeichert, so dass ich hier keine Daten weitergebe.

Wer Fehler findet oder Verbesserungsvorschläge hat, darf sich gerne melden.

Edit: Einen unschönen Fehler habe ich gerade gefunden. Die PHP-Datei mit der ich den OSBN-Feed erzeuge, hat sich noch auf meine Test-Domain bezogen, so dass auf planetlinux.de verlinkt wurde. Das ist nun korrigiert und ich habe eine Weiterleitung auf die richtige Adresse erstellt. Sorry.