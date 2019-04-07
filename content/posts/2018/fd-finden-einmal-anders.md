---
title: Fd - Finden einmal anders
date: 2018-06-17T12:27:00+0100
categories:
- Linux
- OSBN
tags:
- Find
- Alternative
slug: fd-finden-einmal-anders
---
Wer Linux nutzt wird früher oder später auf den Befehl find stoßen. Mit diesem lassen sich, wie der Name schon vermuten lässt, Sachen wie Dateien finden. Vor ein paar Wochen bin ich nun auf die Alternative fd gestoßen, welche gar nicht mal so schlecht ist.

Nehmen wir mal an, wir haben den Ordner "Projekt" auf der Festplatte. In diesem befindet sich eine Datei die wir dringend brauchen und von der wir nur wissen, dass sie den Namen README hat. Aber nicht ob .md, .doc. oder .txt. Mit find würde man wohl in das Projekt-Verzeichnis wechseln und dort find . -iname 'README*' ausführen. Bei fd reicht schon in das Verzeichnis zu wechseln und fd README auszuführen (wer will kann natürlich auch das Verzeichnis angeben. Zum Beispiel find README /home/nutzer/Projekt). Fd sucht hier automatisch rekursiv alles in dem irgenwie README vorkommt. Somit wird zum Beispiel README.md oder README.gz gefunden. Aber auch Verzeichnisse wie ./README/Anleitung.doc. Wer nur nach Dateien suchen will, kann den Parameter -tf verwenden. Wenn nur Verzeichnisse gesucht werden sollen -td.

Nehmen wir als nächstes Beispiel einmal an, wir suchen nach einer Datei von der wir nur wissen, dass Sie die Endung .md hat. Mit find würde mal wohl find . -type f -name '*.md' nutzen. Mit fd reicht fd *.md.

Das sind jetzt nur einmal zwei Beispiele in denen ich fd find vorziehen würde. Ist fd nun ein vollwertiger Ersatz für find? Definitiv nicht. Denn Sachen wie find -inum 123456789 sind unter fd nicht möglich. Aber für das allgemeine Suchen von Dateien reicht fd locker aus. Zudem ist fd auch deutlich schneller beim Liefern der Suchergebnisse als find. Hat fd auch Nachteile? Kommt wohl auf die eigene Sichtweise an. Fd sollte zum einen in keiner Standardinstallation zu finden sein. Zum anderen wird als Abhängigkeit zum Erstellen von fd Rust benötigt. Die schlägt, zumindest unter Arch, mit etwa mehr als 240 MB zu buche. Rust kann man allerdings hinterher gefahrlos wieder entfernen.
