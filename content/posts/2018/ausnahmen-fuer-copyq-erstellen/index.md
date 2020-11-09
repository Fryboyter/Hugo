---
title: Ausnahmen für CopyQ erstellen
date: 2018-08-04T12:11:00+0100
categories:
- Linux
- OSBN
tags:
- CopyQ
- Ausnahme
slug: ausnahmen-fuer-copyq-erstellen
---
Für meine Passwörter nutze ich aktuell den Passwortsafe [KeepassXC](https://keepassxc.org). Leider habe ich ab und zu die schlechte Angewohnheit Passwörter einfach zu kopieren, so dass diese in Klipper (Zwischenablage unter KDE Plasma) landen. Was beides irgendwie blöd ist.

Leider lassen sich bei Klipper keine Ausnahmen für bestimmte Programme definieren und KeePassXC kann auch in Verbindung mit Klipper die betreffenden Einträge nicht nach X Sekunden automatisch entfernen (was sich aber hoffentlich bald™ dank eines [Pull Request](https://github.com/keepassxreboot/keepassxc/pull/1969) ändern sollte). Trotzdem bin ich jetzt auf [CopyQ](https://hluk.github.io/CopyQ) umgestiegen, da diese Alternative einfach mehr Funktionen bietet und allgemein weniger Probleme macht.

Um zu Verhindern, dass KeePassXC in Verbindung mit CopyQ Einträge in der Zwischenablage erzeugt, öffnet man CopyQ und drückt F6. Über "Hinzufügen" erstellt man jetzt einen neuen Befehl. Der Name ist hier frei wählbar. Unter "Art der Aktion" wählen wir "Automatisch" aus. Unter "Element erfassen" tragen wir bei Fenster "- KeePassXC" (ohne die ") ein, da in der Titelzeile von Keepass immer Datenbankname - KeePassXC steht. Als Befehl geben wir nun noch "copyq ignore" ein (ebenfalls wieder ohne ") und speichern das ganze. Kopiert man nun die Zugangsdaten direkt, sollten diese nicht mehr in der Zwischenablage von CopyQ landen.

Bleibt nur die Frage, was macht man mit Klipper? Früher war Klipper einfach ein extra Tool, dass man beenden und entfernen konnte. Aktuell ist es fester Bestandteil von Plasma. Aber auch hier kann man Klipper noch deaktivieren. Auf den ersten Blick ist es nur nicht ganz so offensichtlich. Neben den Symbolen im Tray sollte ein Pfeil angezeigt werden. Wenn man mit der rechten Maustaste darauf klickt, sollte "Einstellungen für den Systemabschnitt der Kontrollleiste" angezeigt werden. Dies wählt man aus und findet dann unter "Allgemein" den Punkt "Zwischenablage". Hier entfernt man die Auswahl und klickt auf "Anwenden". Anschließend macht man am besten einen Neustart, da sonst Klipper erst einmal im Hintergrund weiterläuft.
