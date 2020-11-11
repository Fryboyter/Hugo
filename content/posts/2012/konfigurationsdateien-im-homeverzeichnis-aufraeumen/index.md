---
title: Konfigurationsdateien im Homeverzeichnis aufräumen
date: 2012-07-13T10:43:00+0100
categories:
- Linux
- OSBN
tags:
- Konfigurationsdateien
- Homeverzeichis
- Auräumen
- Dotfiles
slug: konfigurationsdateien-im-homeverzeichnis-aufraeumen
---
In meinem Homeverzeichnis unter Linux stapeln sich inzwischen schon die Dotfiles. Also die Konfigurationsdateien mit einem Punkt am Anfang des Namens. Irgendwann habe ich mir die Frage gestellt, ob man die Dateien nicht in ein Unterverzeichnis verschieben kann, damit das Verzeichnis etwas übersichtlicher wird. Ein komplettes Ausblenden aller versteckten Dateien bzw. Verzeichnisse (alle mit einem Punkt am Anfang der Bezeichnung) kommt für mich nicht in Frage, da ich auf manche Verzeichnisse regelmäßig zugreife.

Als erstes bin ich auf [libetc](http://ordiluc.net/fs/libetc "libetc") gestoßen. Damit konnte man die Dotfiles in ein Unterverzeichnis packen alle Anfragen wurden auf diese Unterverzeichnis umgeleitet. Da libetc aber zum einen gar nicht mehr betreut wird und man es zum anderen nicht mehr unter Arch Linux installiert bekommt, habe ich mich weiter auf die Suche gemacht.

Und bin fündig geworden. [Rewritefs](https://github.com/sloonz/rewritefs "rewritefs") sollte die Lösung sein. Die letzte Aktivität bei dem Projekt war zumindest noch 2012. Rewritefs nutzt [FUSE](http://de.wikipedia.org/wiki/Filesystem_in_Userspace "FUSE") und macht in etwa das was [mod_rewrite](http://de.wikipedia.org/wiki/Rewrite-Engine "mod_rewrite") unter Apache macht.

Mal schauen, ob es mir am Wochenende das System zerlegt, oder ob ich etwas mehr Ordnung in mein Homeverzeichnis bringen kann.
