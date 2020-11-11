---
title: Alternative zu MySQL-Workbench
date: 2012-10-23T22:31:00+0100
categories:
- Linux
- OSBN
tags:
- Alternative
- MySQL-Workbench
- Navicat
- DBeaver
- HeidiSQL
slug: alternative-zu-mysql-workbench
---
Wenn ich größere Sachen an einer MySQL-Datenbank mache, habe ich bisher immer [MySQL-Workbench](http://www.mysql.de/products/workbench "MySQL Workbench") eingesetzt. An sich finde ich das Programm recht gut. Da sich durch ein Update die Bezeichnung einiger Python-Pakete unter Arch Linux geändert haben, war eine kurze Neuinstallation von MySQL-Workbench fällig. Sagte ich kurz? Genau das ist der Punkt, an dem ich das Programm am liebsten aus dem Fenster werfen würde. Das bauen des Paketes dauert gut 30 Minuten. Während der Rechner also fleißig vor sich hin baut, habe ich mir mal die Alternativen zu MySQL-Workbench angesehen. [Navicat](http://www.navicat.com "Navicat") finde ich zwar gut, aber für das was ich daheim mache, zu teuer. [HeidiSQL](http://www.heidisql.com "HeidiSQL") läuft zwar mit Wine, aber darauf möchte ich verzichten. Zufällig bin ich dann auf (DBeaver](http://dbeaver.jkiss.org "DBeaver") gestoßen. Und so wie es aussieht, wird MySQL-Workbench wohl von der Platte fliegen, da es innerhalb weniger Sekunden installiert ist. Lediglich der Start könnte etwas schneller sein.

Bisher habe ich mit DBeaver nur etwas herum gespielt. Aber was ich gesehen habe, hat mir gefallen. Das Teil kommt nicht nur mit MySQL sondern auch mit vielen anderen Datenbanken zurecht. PostgreSQL, Oracle und Informix. Nur um mal ein paar Beispiele zu nennen. Somit könnte ich auch die Datenbanken auf der Arbeit von daheim aus quälen... :D Ebenfalls gut finde ich, dass man damit automatisch einen SSH-Tunnel aufbauen kann, um sich darüber mit externen Datenbankservern zu verbinden. ERD Diagramme werden auf den ersten Blick ebenfalls unterstützt. Und der SQL-Editor für die Statements scheint auch das zu machen, was ich will.

Da DBeaver in Java erstellt wurde (was vermutlich die relativ lange Ladezeit erklärt), läuft es nicht nur unter Linux, sondern auch unter Windows, Mac, Solaris usw. Lange Rede, kurzer Sinn, wer von MySQL-Workbench weg will oder einfach mal etwas neues probieren will, sollte mal einen Blick auf den DBeaver werfen.
