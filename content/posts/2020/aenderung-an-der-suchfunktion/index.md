---
title: Änderung an der Suchfunktion
date: 2020-11-21T13:56:31+0100
categories:
- OSBN
- Allgemein
tags:
- Hugo 
- Suchfunktion
- JSON
slug: aenderung-an-der-suchfunktion
---
Letztes Jahr hatte ich in https://fryboyter.de eine Suchfunktion [eingebaut](/fryboyter-um-suchfunktion-erweitert/), die DuckDuckGo nutzt. So wirklich glücklich war ich damit nie, da ich somit auf Dritte angewiesen bin.

Daher habe ich vor ein paar Tagen die Suchfunktion umgebaut. Über https://fryboyter.de/search/ bzw. über das Lupen-Symbol im Footer der Seite ist nun die neue Suchfunktion erreichbar die unabhängig von Dritten ist. Intern wird hierfür eine JSON-Datei erzeugt, die als Datenquelle dient. Mittels eines kleinen Java-Scripts lässt sich diese Datei durchsuchen. Wer also die Suchfunktion nutzen will, muss Javascript aktivieren. Zumindest bei genannten Link.

Einen kleinen Nachteil hat das ganze natürlich auch. Die JSON-Datei wird auf den Rechner des jeweiligen Nutzers heruntergeladen, da die Suche lokal erfolgt. Hierbei werden aktuell etwas mehr als 300 kB übertragen. In Anbetracht dessen, dass heutzutage viele Internetseiten an sich um ein Vielfaches größer sind und die Datei nur bei Aufruf des genannten Links heruntergeladen wird, finde ich die Datenmenge vertretbar.

Die Änderung basiert auf der Anleitung von [https://weitblick.org/post/simple-static-site-search-hugo-jamstack/](https://weitblick.org/post/simple-static-site-search-hugo-jamstack/). Vielen Dank dafür.
