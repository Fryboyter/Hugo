---
title: Pakete unter Arch im Ram erstellen
date: 2015-03-01T21:04:00+0100
categories:
- Linux
- OSBN
tags:
- Arch Linux
- Ram Disk
- Makepkg.conf
slug: pakete-unter-arch-im-ram-erstellen
---
Um das Bauen der Pakete unter Arch zu beschleunigen kann man die Paketverwaltung anweisen dies im Arbeitsspeicher zu tun.

Hierzu erstellt man in der /etc/fstab erst einmal folgenden Eintrag.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">tmpfs    /scratch    tmpfs    nodev,size=4G    0 0</code>
</pre>

Anstelle von /scratch kann man jederzeit auch ein anderes Verzeichnis angeben in dem der Arbeitsspeicher gemountet wird. Size= kann man weglassen. Allerdings werden dann bis zu 50 Prozent des vorhandenen Arbeitsspeicher genutzt.

Nachdem wir die Datei abgespeichert haben, schalten wir den Eintrag mittels mount -a scharf. Nun muss noch die Datei /etc/makepkg.conf angepasst werden. In dieser suchen wir nach #BUILDDIR= und entfernen das # am Anfang der Zeile unter ändern alles nach dem = auf /scratch (bzw. das Verzeichnis das wir in der /etc/fstab angegeben haben, so dass BUILDDIR=/sratch dabei herauskommen sollte und speichern die Datei ab.

Pakete die nun aus den Sourcecode erstellt werden, z. B. aus AUR sollten nun um einiges schneller gebaut werden als z. B. auf der HDD.
