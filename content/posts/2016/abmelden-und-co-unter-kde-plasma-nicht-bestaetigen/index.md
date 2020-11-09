---
title: Abmelden und Co. unter KDE Plasma nicht bestätigen
date: 2016-02-21T22:13:00+0100
categories:
- Linux
- OSBN
tags:
- Plasma
- KDE
- Abmelden
slug: abmelden-und-co-unter-kde-plasma-nicht-bestaetigen
---
Eigentlich mag ich KDE Plasma. Aber ein paar Kleinigkeiten nerven mich auch. So zum Beispiel dass man in der Standardkonfiguration das Herunterfahren, Neustarten bzw. Abmelden bestätigen muss. Oder man wartet bis der 30-sekündige Timer abgelaufen ist. Beides finde ich weniger gut. Perfekt wäre es, wenn man den Timer einstellen könnte. Sagen wir auf 3 Sekunden. Somit hat man, wenn man sich dann doch einmal verklicken sollte, noch die Chance den Vorgang abzubrechen. Ein Ändern des Timers sieht das KDE-Team aber scheinbar nicht vor. Wieso auch immer. Aber zumindest gibt es eine Möglichkeit den Timer komplett außer Kraft zu setzen. Hierzu editiert man einfach die Datei ~/.config/ksmserverrc. Unter [General] findet man den Eintrag confirmLogout=true, welchen man auf false setzt und die Datei wieder abspeichert. Alternativ kann man im in den Systemeinstellungen von KDE Plasma auch unter Arbeitsbereich "Starten und Beenden" auswählen. Dort klickt man dann links auf "Arbeitsflächen-Sitzung" und wählt dann rechts "Abmeldung bestätigen" ab. und speichert die Änderung.
