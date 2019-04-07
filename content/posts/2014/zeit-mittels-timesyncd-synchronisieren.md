---
title: Zeit mittels timesyncd synchronisieren
date: 2014-08-26T09:45:00+0100
categories:
- Linux
- OSBN
tags:
- Uhrzeit
- Timesyncd
- Systemd
slug: zeit-mittels-timesyncd-synchronisieren
---
Vor ein paar Minuten ist mit aufgefallen, dass die Uhr unter lxde um ein paar Minuten falsch läuft. Wie es sich herausgestellt hat, hatte ich schlicht und ergreifend vergessen NTPD zu [installieren](https://wiki.archlinux.de/title/NTP "NTP Arch"). Bei der Gelegenheit habe ich jetzt allerdings timesyncd getestet. Dies ist ein Service aus dem systemd-Projekt (nicht dem init-Dienst) welcher für meine Anforderungen das gleiche wie NTP macht. Es gleicht die Uhr meines Rechners mit einem Zeitserver im Internet ab.

Als erstes habe ich mir die Konfigurationsdatei /etc/systemd/timesyncd.conf vorgenommen. Diese ist im Auslieferungszustand sehr übersichtlich.

<pre class="line-numbers" style="white-space:pre-wrap;"><code class="language-bash">#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.
#
# See timesyncd.conf(5) for details

[Time]
#Servers=time1.google.com time2.google.com time3.google.com time4.google.com</code></pre>

Eigentlich muss man in der letzten Zeile nur das # entfernen und die Datei speichern.

Als nächstes habe ich dann mittels "systemctl start timesyncd" den Service gestartet. Da es keinerlei Beschwerden gab, folgte ein "systemctl enable timesyncd" um den Service automatisch zu starten. Abschließend habe ich den Rechner neu gestartet. Und die Uhr lief trotzdem um ein paar Minuten falsch... Also mal Tante Google fragen. Nach wenigen Sekunden hatte ich die Antwort. Damit timesyncd funktioniert muss auch systemd-networkd laufen. Da ich aber netctl für meine Netzwerkverbindungen nutze, ist mir das aber nicht so recht. Aber vielleicht reicht es ja, wenn systemd-networkd nur läuft aber nicht konfiguriert ist... Probieren wir es aus und aktivieren wir den Dienst mittels "systemctl enable systemd-networkd" und starten die Büchse neu. Und schwupps funktioniert timesyncd, obwohl ich netctl nutze. Vermutlich werde ich aber trotzdem wieder auf ntpd umschwenken, da ich damit systemd-networkd nicht laufen lassen muss.
