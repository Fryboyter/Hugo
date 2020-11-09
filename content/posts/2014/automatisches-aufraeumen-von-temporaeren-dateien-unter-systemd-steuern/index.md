---
title: Automatisches Aufräumen von temporären Dateien unter systemd steuern
date: 2014-08-27T20:17:00+0100
categories:
- Linux
- OSBN
tags:
- Temporäre Dateien
- Systemd
- Aufräumen
slug: automatisches-aufraeumen-von-temporaeren-dateien-unter-systemd-steuern
---
In den letzten Wochen war es mal wieder hip gegen systemd zu sticheln. Einige Personen hatten es zum Beispiel auf den Service systemd-tmpfiles-clean abgesehen. Mit diesem werden temporäre Dateien nach einer bestimmten Zeitspanne automatisch gelöscht. Die Standardeinstellung für /tmp ist 10 Tage, die für /var/tmp 30 Tage.

Es wurde nun argumentiert, dass diese Einstellungen für die meisten Nutzer blödsinnig wären. Wie gut, dass man etwas dagegen machen kann. Fangen wir mal damit an, die Fristen auf die persönlichen Bedürfnisse anzupassen. Die betreffende Konfigurationsdatei findet man unter /usr/lib/tmpfiles.d/ und nennt sich tmp.conf. Diese sieht bei mir wie folgt aus.

<pre class="line-numbers" style="white-space:pre-wrap;"><code class="language-bash">#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.
#
# See tmpfiles.d(5) for details

# Clear tmp directories separately, to make them easier to override
d /tmp 1777 root root 10d
d /var/tmp 1777 root root 30d

# Exclude namespace mountpoints created with PrivateTmp=yes
x /tmp/systemd-private-%b-*
X /tmp/systemd-private-%b-*/tmp
x /var/tmp/systemd-private-%b-*
X /var/tmp/systemd-private-%b-*/tmp</code></pre>

Die ersten beiden Zeilen setzen sich wie folgt zusammen. |Typ|Pfad|Rechte|UID|GID|Alter|. Für viele ist vermutlich das Alter interessant ab dem gelöscht wird. Hier kann man sich entsprechend austoben. Mögliche Zeiteinheiten sind s, min, h, d, w, ms, m, us. Diese müssen ohne Lehrzeichen angegeben werden. Also z. B. 10d oder 10d12h.

Will man z. B. ein Unterverzeichnis vom automatischen Bereinigen ausnehmen ist der Typ x, wie man es im zweiten Block sehen kann, die Wahl der Waffe.

Unter [http://www.freedesktop.org/software/systemd/man/tmpfiles.d.html](http://www.freedesktop.org/software/systemd/man/tmpfiles.d.html "http://www.freedesktop.org/software/systemd/man/tmpfiles.d.html") (englisch) kann man sich den ganzen Spaß noch genauer und ausführlicher durchlesen.

Was aber, wenn man gar kein automatisches Bereinigen der temporären Dateien wünscht? Am einfachsten ist es wohl den Service einfach zu deaktivieren.

Abschließend bleibt mir eigentlich nur noch eines zu sagen. **Dieses** Argument gegen systemd ist eigentlich gar kein Argument. Es zeigt eigentlich nur, dass sich viele systemd-Gegner nicht wirklich mit systemd-Projekt beschäftigt haben. Und nein, systemd ist trotz allem nicht der heilige Gral. Ich musste mich auch schon einige Zeit mit der Meldung "a stop stop ist running for User Manager for UID 1026" und dem damit verbundenen Countdown von 90 Sekunden beim Herunterfahren meines Hauptrechners herumschlagen.
