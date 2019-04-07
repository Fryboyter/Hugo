---
title: Fritz!WLAN Stick AC 860 funktioniert nach Standby-Modus nicht mehr
date: 2018-12-22T11:55:00+0100
categories:
- Linux
- OSBN
tags:
- Fritz
- AC 860
- Standby
slug: fritz-wlan-stick-ac-860-funktioniert-nach-standby-modus-nicht-mehr
---
Vor ein paar Tagen hatte ich einen Artikel über den Fritz!WLAN Stick AC 860 veröffentlicht. Zwischenzeitlich habe ich leider feststellen müssen, dass die WLAN-Verbindung nicht wieder aufgebaut wird, wenn der Rechner aus dem Standby-Modus geholt wird.

Die Lösung oder besser gesagt der Workaround ist allerdings relativ simpel. Ich habe mir unter /etc/systemd/system einfach zwei neue Service-Dateien mit folgenden Inhalt erstellt und diese dann aktiviert.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code>[Unit]
Description=WLAN vor Standby deakivieren
Before=sleep.target

[Service]
Type=oneshot
ExecStart=/usr/bin/systemctl stop netctl@wlan.service ; /usr/bin/rmmod mt76x2u

[Install]
WantedBy=sleep.target</code>
</pre>

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=WLAN nach Standby aktivieren
After=suspend.target

[Service]
Type=oneshot
ExecStart=/sbin/modprobe mt76x2u ; /usr/bin/systemctl start netctl@wlan.service

[Install]
WantedBy=suspend.target</code>
</pre>

Die erste Service-Datei deaktiviert die Netzwerkverbindung bevor der Rechner schlafen gelegt wird. Die zweit startet die Netzwerkverbindung wieder wenn der Rechner aus dem Standby-Modus geholt wurde.
