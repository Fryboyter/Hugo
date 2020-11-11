---
title: Arch Linux setzt auf systemd
date: 2012-08-15T09:46:00+0100
categories:
- Linux
- OSBN
tags:
- Arch Linux
- Systemd
slug: arch-linux-setzt-auf-systemd
---
Nun ist es [offiziell](http://mailman.archlinux.org/pipermail/arch-dev-public/2012-August/023389.html "Arch Linux wechselt zu systemd"). Auch Arch Linux wird zu [systemd](http://de.wikipedia.org/wiki/Systemd "systemd") wechseln. Diesen Schritt sind schon einige Distributionen wie Mandriva, Mageia, Fedora oder OpenSuse gegangen. Ich finde die Entscheidung gut.

In absehbarer Zeit wird wohl alles unter systemd laufen (einige Unit scheinen noch zu fehlen) und die rc.conf vermutlich wegfallen. Für einige Archer ist das scheinbar ein Horrorszenario, da angeblich Arch Linux ohne rc.conf nicht mehr Arch Linux ist. Allen McRae hat dazu und zu diversen anderen Änderungen in der letzten Zeit (wie z. B. der Symlink von /lib nach /usr/lib), die auf Kritik bei den Anwendern gestoßen sind, einen guten [Beitrag](http://allanmcrae.com/2012/08/are-we-removing-what-defines-arch-linux "Wird das entfernt, was Arch Linux definiert") in seinem Blog geschrieben.

Ich werde dies mal als Anlass nehmen und meine Arch-Linux-Installation so weit wie möglich auf systemd umstellen. Bisher läuft hier noch ein Mischbetrieb aus einer alten rc.conf mit allem drum und dran und systemd.

Nachtrag (21.08.2012): Tomegun (einer der Entwickler) hat sich im englischsprachigen Arch-Linux-Forum dazu [geäußert](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530 "Roadmap Arch systemd") wie der Umstieg bisher geplant ist und hat auch einige Punkte genannt warum umgestiegen wird.
