---
title: Pacman XferCommand
date: 2012-06-29T17:49:00+0100
categories:
- Linux
- OSBN
tags:
- Pacman
- XferCommand
- Snarf
slug: pacman-xfercommand
---
Ich setze unter pacman (Paketverwaltung von Arch Linux) seit einiger Zeit nicht den internen Downloadmechanismus sondern snarf ein. Das gibt bis zur Version 4.0.3 von pacman auch gut. Seit dem gab es diverse 404-Fehler beim Aktualisieren der Pakete. Snarf findet also irgendetwas nicht und bricht deshalb ab. Gerade habe ich in einem lichten Moment die Lösung gefunden. Mittels pacman -Syu --debug bin ich dem Problem auf die Spur gekommen. Snarf hat die Signatur-Dateien der Datenbanken (z. B. core.db.sig) nicht gefunden. Kein Wunder, bisher sind ja nur die Pakete an sich signiert und die Datenbanken kommen erst später an die Reihe. Um trotzdem eines der XferCommand-Einträge in der /etc/pacman.conf zu nutzen muss man in selbiger bei den eingetragenen Paketquellen bei beim SigLevel noch DatabaseNever hinzufügen, so dass es wie folgt aussieht.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[core]
SigLevel = PackageRequired DatabaseNever
Include = /etc/pacman.d/mirrorlist</code>
</pre>

Und schon funktionieren die XferCommand-Einträge wieder.
