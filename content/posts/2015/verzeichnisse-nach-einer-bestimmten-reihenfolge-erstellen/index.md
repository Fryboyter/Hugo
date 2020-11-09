---
title: Verzeichnisse nach einer bestimmten Reihenfolge erstellen
date: 2015-12-12T14:31:00+0100
categories:
- Linux
- OSBN
tags:
- Verzeichnisse
- Reihenfolge
- Erstellen
slug: verzeichnisse-nach-einer-bestimmten-reihenfolge-erstellen
---
Neues Projekt, neue Probleme. Derzeit bin ich dabei, bestimmte Texte so mit Markdown zu formatieren, dass ich sie mittels pandoc in eine EPUB- sowie eine PDF-Datei umwandeln kann. Da es sich bei den Texten um mehr als 100 Stück handelt brauche ich hierfür eine gewisse Ordnung, sonst verliere ich die Übersicht. Von daher habe ich erste einmal ein Arbeitsverzeichnis angelegt. In diesem sollen dann Unterverzeichnisse von A bis Z angelegt werden in welche dann die Markdowndateien abgespeichert werden. Nur wie lege ich diese jetzt am besten an? Mittels mkdir A, mkdir B, mkdir C? Darauf würde ich gerne verzichten. Also eine Schleife? Das würde mir zumindest einiges an Arbeit ersparen. Die Lösung ist in diesem Fall aber noch einfacher. Das ganze lässt sich sogar mit mkdir direkt lösen. So reicht es aus mkdir {A..Z} auszuführen und schwups hat man Verzeichnisse von A bis Z angelegt. Braucht man Verzeichnisse mit Zahlen nimmt man beispielsweise einfach mkdir {1..10} und erstellt damit Verzeichnisse von 1 bis 10. Das ganze nennt man Brace Expansion. Damit lassen sich auch noch komplexere bzw. andere Sachen anstellen. So kann man beispielsweise durch mv test.{txt,bak} die Datei test.txt in test.bak umbenennen.
