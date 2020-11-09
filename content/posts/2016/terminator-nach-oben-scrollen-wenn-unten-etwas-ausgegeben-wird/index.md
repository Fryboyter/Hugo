---
title: Terminator - Nach oben scrollen wenn unten etwas ausgegeben wird
date: 2016-03-29T21:02:00+0100
categories:
- Linux
- OSBN
tags:
- Terminator
- Scrollen
- Bildlauf
slug: terminator-nach-oben-scrollen-wenn-unten-etwas-ausgegeben-wird
---
Baut man beispielsweise ein Paket aus dem AUR, bekommt man in der Regel eine längere Ausgabe in der Shell angezeigt. Ab und zu kommt es vor, dass mir hier diverse Stellen auffallen, welche ich mir ansehen möchte bevor das Paket tatsächlich erstellt wurde. Unter dem von mir verwendeten Terminal-Emulator Terminator scrolle ich dann nach oben um dann quasi sofort wieder am Ende der Ausgabe zu landen, weil eine neue Zeile ausgegeben wurde.

Da ich in der aktuellen Einstellung von Terminator nur maximal 500 Zeilen nach oben scrollen kann und beim erstellen von Paketen oft mehr zusammenkommen ist das oft blöd. Vor allem wenn sich die interessante Stellen recht weit oben befindet.

Da Terminator Richtung "eierlegende Wollmilchsau" geht, war ich mir sicher, dass man das Verhalten irgendwie ändern kann. In den Einstellungen habe ich aber nichts gefunden. Wie ich nun feststellen musste, habe ich einfach an der falschen Stelle gesucht. Ruft man die Einstellungen auf muss man den Reiter "Profile" auswählen. Hier findet man recht dann den Reiter "Bildlauf". Entfernt man dort den Haken bei "Bildlauf bei Ausgabe" kann man problemlos nach oben scrollen wenn am Ende eine Ausgabe erfolgt.
