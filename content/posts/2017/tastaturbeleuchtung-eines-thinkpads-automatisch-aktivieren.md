---
title: Tastaturbeleuchtung eines Thinkpads automatisch aktivieren
date: 2017-01-02T17:27:00+0100
categories:
- Linux
- OSBN
tags:
- Tastatur
- Beleuchtung
- Thinkpad
- X230
slug: tastaturbeleuchtung-eines-thinkpads-automatisch-aktivieren
---
Mir wäre es ganz lieb, wenn sich mein X230 Notebook den Zustand das Tastaturbeleuchtung merken würde und dieser Zustand nach einem Reboot auch wiederherstellt wird. Klappt aber nicht. Daher habe ich nachgeholfen.

Kurzerhand habe ich einfach eine Service-Datei für systemd erstellt. Ich habe sie mal backlight.service genannt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Tastaturbeleuchtung automatisch aktivieren

[Service]
Type=simple
ExecStart=/bin/bash -c 'echo 1 &gt; /sys/devices/platform/thinkpad_acpi/leds/tpacpi::kbd_backlight/brightness'

[Install]
WantedBy=multi-user.target</code>
</pre>

Interessant ist hier im Grunde genommen nur die ExecStart-Zeile. Hier wir der Befehl ausgeführt, der die Tastaturbeleuchtung auf Stufe 1 aktiviert (Stufe 2 wäre die stärkste Beleuchtung und Stufe 3 würde noch die Beleuchtung im Rahmen des Displays hinzuschalten). Klappt soweit auch. Da das Notebook verschlüsselt ist, wäre es mir auch recht, wenn die Tastatur schon bei der Eingabe des Passworts klappen würde. Scheinbar gibt es aber kein passendes Target hierfür.
