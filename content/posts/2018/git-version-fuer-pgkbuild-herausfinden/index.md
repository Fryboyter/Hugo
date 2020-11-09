---
title: Git-Version für PGKBUILD herausfinden
date: 2018-02-27T23:52:00+0100
categories:
- Linux
- OSBN
tags:
- Git
- Version
- PKGBUILD
slug: git-version-fuer-pgkbuild-herausfinden
---
Im Arch User Repository, kurz AUR, gibt es einige Paket mit dem Zusatz -git im Namen. Hiermit werden nicht die stabilen Versionen sondern Entwicklerversionen installiert.

Nehmen wir einmal die PKGBUILD-Datei von keepassxc-git als Beispiel. In dieser findet man die Zeile pkgver=2.2.4.r431.g46c58b32. Egal wie oft man nun KeepassXC über diese PKGBUILD-Datei installiert, landet man immer beim gleichen festgelegten Entwicklungsstand und nicht beim derzeit aktuellen. Was aber, wenn man sich genau diesen installieren will? Im Grunde genommen muss man die Zeile pkgver= einfach nur anpassen. Aber was muss man in solch einem Fall eintragen? Eine Lösung wäre folgendes Vorgehen:

- Mittels "git clone [https://github.com/keepassxreboot/keepassxc.git](https://github.com/keepassxreboot/keepassxc.git)" den Sourcecode auf den eigenen Rechner kopieren. Den betreffenden Link findet man in dem man auf der jeweiligen Github-Seite auf "Clone or download" klickt.

- Danach wechselt man in das erstellte Verzeichnis. In diesem Fall keepassxc und führt dort "git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'" aus. Hier wird dann aktuell "2.3.0.r10.g3c274135" ausgegeben, da die Veröffentlichung von Version 2.3.0 ansteht.

- Abschließend ändert man nun in der PKGBUILD-Datei die Zeile pkgver= entsprechend ab und kann sich so die aktuelle Entwicklerversion installieren.

- Um die Version in der PKGBUILD-Datei erneut zu aktualisieren, reicht es in das Verzeichnis keepassxc zu wechseln und dort "git pull" und danach "git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g" auszuführen. Git clone ist hier nicht nötig.

Da Git-Versionen aber nicht unbedingt stabil sind, sollte man aber abwägen ob man sich solch eine Version installiert oder nicht.
