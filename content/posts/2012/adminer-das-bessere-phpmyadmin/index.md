---
title: Adminer - das bessere phpMyAdmin?
date: 2012-10-07T22:21:00+0100
categories:
- OSBN
- Allgemein
tags:
- Adminer
- Datenbanken
- Verwalten
slug: adminer-das-bessere-phpmyadmin
---
Seit ich bei uberspace.de bin, nutze ich das bekannte [phpMyAdmin](http://www.phpmyadmin.net "phpMyAdmin") zum Verwalten von MySQL-Datenbanken nicht mehr. Warum? Aus zwei Gründen. Zum einen weil ich für größere Sachen das Programm MySQL Workbench nutze, welches sich über SSH mit der Datenbank verbindet (ssh -L 3306:127.0.0.1:3306 $benutzer@$server.uberspace.de). Und zum anderen weil ich im Wiki die phpMyAdmin-Alternative [Adminer](http://www.adminer.org/de "Adminer") gefunden habe. Damit lässt sich, zumindest subjektiv, viel angenehmer an einer Datenbank werkeln als mit phpMyadmin. Wer also eine Alternative sucht, aber keine Verbindung von außen mit der Datenbank aufnehmen kann, sollte sich Adminer zumindest einmal ansehen.

Nachtrag 08.10.12: Heute morgen hat mich eine E-Mail erreicht (wieso eigentlich E-Mail und kein Kommentar zum Artikel?), in der gefragt wurde, ob Adminer wirklich nur aus einer Datei und nicht aus mehreren wie bei phpMyAdmin besteht. Da das vielleicht auch für andere interessant ist beantworte ich die Frage hier. Ja das ist so. Adminer besteht nur aus einer PHP-Datei.