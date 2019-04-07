---
title: KB3133977 auf einem Dualbootsystem installieren
date: 2016-04-24T09:50:00+0100
categories:
- Allgemein
tags:
- Dualboot
- Linux
- Windows
- KB3133977
slug: kb3133977-auf-einem-dualbootsystem-installieren
---
Heute habe ich seit einiger Zeit mal wieder Windows gebootet. Logischerweise haben sich hier einige Updates angesammelt, die ich lieber gleich mal installiert habe. Bis auf KB3133977 hat das auch geklappt. Nur dieses verschissene Update hat sich mit Händen und Füßen geweigert. Das Update braucht einen Neustart. Und hier gab es jedes mal den Fehler 80004005. Dieser bedeutet grob gesagt, es ist ein unbekannter Fehler beim Windows-Update passiert. Wer hätte das gedacht...

Nach einigem hin und her habe ich das Problem gefunden. Ich habe auf dem betreffenden Rechner sowohl Arch Linux als auch Windows 7 HP installiert (jeweils auf einer eigenen SSD). Gestartet werden beide mittels syslinux. Und genau das mag das Update nicht. Es ist scheinbar mal wieder eines dieser Updates der Marke "du darfst keine anderen Götter / Betriebssysteme haben neben mir". Als ich Windows direkt über UEFI gebootet hatte (sowohl zum Einspielen des Updates als auch beim benötigten Neustart) wurde das Update anstandslos installiert. Warum einfach, wenn es auch kompliziert geht?