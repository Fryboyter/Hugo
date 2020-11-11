---
title: Temporäre Tabellen unter MySQL erstellen
date: 2013-01-27T14:58:00+0100
categories:
- OSBN
- Allgemein
tags:
- Temporäre Tabellen
- MySQL
slug: temporaere-tabellen-unter-mysql-erstellen
---
Am Freitag war ich mal wieder in der Situation etwas an einer Datenbank ändern zu müssen. Und das ohne Netz und doppelten Boden. Sprich die Datensicherung war schon ein paar Stunden alt und für eine Testdatenbank war keine Zeit. Da die Änderungen nicht ganz ohne waren, habe ich mir trotzdem einen Sicherheitsgurt eingebaut. Ich habe mir einfach eine temporärer Tabelle angelegt. Das ganze ist recht simpel.

>CREATE TEMPORARY TABLE test (SELECT * from nutzer)

Bei diesem Beispiel wird also die temporäre Tabelle test in der Datenbank erstellt. Und zwar mit allem, was in der Tabelle nutzer vorhanden ist. Auf diese temporärer Tabelle habe ich dann mein Script losgelassen, das diverse Änderungen durchgeführt hat. Nachdem das einwandfrei geklappt hat, habe ich es dann auf die richtige Tabelle losgelassen. Einen DROP kann man sich übrigens schenken, da die temporären Tabellen nur so lange halten, wie man mit der Datenbank verbunden ist. Naja im Grunde nichts besonderes, aber vielleicht kann es ja jemand mal gebrauchen.