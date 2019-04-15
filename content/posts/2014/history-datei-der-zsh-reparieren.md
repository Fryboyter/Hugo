---
title: History-Datei der ZSH reparieren
date: 2014-07-12T11:34:00+0100
categories:
- Linux
- OSBN
tags:
- History
- ZSH
- Reparieren
---
Seit einiger Zeit habe ich das Problem, dass wenn ich Arch Linux herunterfahre, die Meldung "a stop stop ist running for User Manager for UID 1026" erscheint und das System erst einmal 90 Sekunden wartet und dann erst mit dem Herunterfahren weitermacht. Die UID entspricht übrigens meinem normalen Benutzerkonto.

Nach längerem hin und her, da mir das <a href="http://freedesktop.org/wiki/Software/systemd/Debugging/#index2h1" title="systemd Debugging">hier</a> beschriebene Debuggin auch nicht weitergeholfen hat, habe ich mal getestet, was passiert wenn ich die Kiste per poweroff -f herunterfahre. Die erste positive Erkenntnis war, dass die Kiste ohne Fehler herunterfährt. Die erste negative Erkenntnis war allerdings, dass es dabei scheinbar die History-Datei von ZSH zerlegt hat. Sobald ich terminator aurufe begrüßt mich die ZSH mit "zsh: corrupt history file /home/benutzer/.zhistory" Tja force hat halt in der Regel immer Nachteile und sollte gut überlegt sein...

Wären in der Datei nicht sehr viele Einträge vorhanden, von denen einige ziemlich komplex sind (zumindest für mich), hätte ich die Datei einfach gelöscht und von Null wieder angefangen. Kommt aus genannten Gründen aber eben nicht in Frage.

Also ist mal wieder Bastelstunde. Die Lösung war aber, vorüber ich heilfroh bin, sehr einfach. Korrekte History-Einträge sind wie folgt aufgebaut.

<pre>
<code class="language-bash">1383417678:0;nano /etc/fstab</code></pre>

Grob gesagt ein Timestamp gefolgt von einem Befehl.

Nachdem ich die ganze Datei durchgegangen bin (habe ich schon gesagt, dass die Datei ziemlich groß ist?) bin ich auf einen Eintrag gestoßen, der sich von den restlichen unterscheidet.

<pre>
<code class="language-bash">^@^@^@^@^@^@^@^@^@^@^@^@^: 1405154859:0;su
</code></pre>

Da mit ansonsten nichts aufgefallen ist, habe ich die Originaldatei erst einmal weggesichert und dann einfach mal das ganze Zeug vor dem Doppelpunkt des betreffenden Eintrags entfernt und die Datei abgespeichert. Und schon gibt es keine Fehlermeldung mehr.
