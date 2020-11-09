---
title: KeePassXC - Autotype außerhalb des Browsers ausführen
date: 2018-08-04T12:43:00+0100
categories:
- Linux
- OSBN
tags:
- KeepassXC
- Autotype
slug: keepassxc-autotype-ausserhalb-des-browsers-ausfuehren
---
Um mich zum Beispiel in einem Forum einzuloggen, nutze ich KeePassXC in Verbindung mit der Erweiterung KeePassXC Browser, die es für die verbreitesten Browser gibt. Hier erfolgt die Zuordnung der Zugangsdaten anhand der in Keepass hinterlegten URL. Was aber wenn es keine URL gibt? Zum Beispiel bei Steam.

Auch hierfür gibt es eine Lösung. In KeePassXC wählt man einfach den betreffenden Eintrag aus und klickt links auf "Auto-Type". Unter "Fenster-Einstellungen" klickt man links auf das Pluszeichen und trägt dann beim Fenstertitel "Steam Login" (ohne ") ein weil dies eben der Titel des Fensters ist. Und klickt anschließend auf "Anwenden". Öffnet man nun Steam und führt den Shortcut für Autotype in KeePassXC aus, sollte es funktionieren. Eigentlich. Bei mir wurde als Benutzername aber immer der Benutzername und das erste Zeichen des Passworts eingetragen (keine Ahnung ob nur ich betroffen bin, oder ob das ein allgemeiner Bug ist). Nach einigen Versuchen habe ich hierfür zumindest einen Workaround gefunden.

Man wählt erneut den betreffenden Eintrag in KeePassXC und öffnet dort wieder die Einstellungen für Auto-Type aus. Unter dem Fenstertitel bei dem wir gerade "Steam Login" eingetragen haben, findet man "Spezielle Auto-Type-Sequenz für dieses Fenster verwenden". Hier sollte {USERNAME}{TAB}{PASSWORD}{ENTER} eingetragen sein. Dies ändert man nun auf {USERNAME}{DELAY 1000}{TAB}{DELAY 1000}{PASSWORD}{ENTER} ab und klickt wieder auf "Anwenden". Nun sollte der Benutzername eingetragen werden, dann wird eine Sekunde gewartet. Dann wird in das Passwortfeld gewechselt und wieder eine Sekunde gewartet. Anschließend wird das ganze noch mit Enter bestätigt. Vermutlich kann man hier die Verzögerung auch noch verkürzen. Aber da es mich nicht stört, lasse ich es erst einmal so.
