---
title: WLAN-Verbindung nach Suspend tot
date: 2014-12-19T01:04:00+0100
categories:
- Linux
- OSBN
tags:
- Wlan
- Suspend
slug: wlan-verbindung-nach-suspend-tot
---
Mein Netbook ist, wie [hier](https://fryboyter.de/mein-netbook-ist-endlich-broadcom-frei "Netbook broadcom-frei") schon geschrieben, mit einem WLAN-USB-Stick von Edimax ausgerüstet. An sich läuft dieser auch sehr zufriedenstellend. Wäre da nur nicht ein Problem wenn ich den Rechner per Suspend schlafen schicke.

In der Datei /etc/systemd/logind.conf habe ich eingestellt, dass sobald der Deckel des Netbooks geschlossen wird der Rechner per Suspend to Ram schlafen geschickt wird. Das funktioniert auch soweit. Wecke ich den Rechner wieder auf funktioniert alles nur die WLAN-Verbindung mag nicht mehr. Hierbei ist mir aufgefallen, dass jedes mal wenn ich den Rechner ins Bett schicke die Anzeige am Stick ausgeht aber nach dem Aufwecken nicht wieder an.

Da ich systemd und für die Netzwerkverbindungen netctl nutze habe ich mir kurzerhand eine Service-Datei gebastelt mit der nach dem Aufwecken auch die WLAN-Verbindung automatisch wieder in einen funktionsfähigen Zustand versetzt wird.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Verbindung mit netctl sichern und wiederherstellen
Before=sleep.target
StopWhenUnneeded=yes


[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/netctl store ; /usr/bin/netctl stop-all
ExecStop=/usr/bin/netctl restore 


[Install]
WantedBy=sleep.target</code>
</pre>

Im Grunde genommen ist das Ganze schnell erklärt. Bevor sleep.target (in dem Fall also Suspend) ausgeführt wird, werden die Befehle abgesetzt, die in der Zeile welche mit ExecStart beginnt stehen. Wenn der Rechner wieder aufgeweckt wird, wird dann noch das ausgeführt, was in der Zeile mit ExecStop eingetragen ist.

Mit netctl store wird abgespeichert, welche Profil gerade aktiv ist. Netctl stop-all stoppt alle Profile. Und netctl restore läd alle Profile wieder, die mit store als aktiv gespreichert wurden. Den Service habe ich dann unter /etc/systemd/system/netctl-restore.service abgespeichert und mittels systemctl enable netctl-restore.service scharf geschaltet. Versetze ich den Rechner nun in Tiefschlaf und wecke ich ihn wieder auf, steht innerhalb weniger Sekunden die WLAN-Verbindung wieder. Einen kleine Schönheitsfehler gibt es aber noch. Ich nutze aus diversen Gründen (wie z. B. wegen der Gema-Blockade bei Youtube) einen VPN-Dienst. Dieser spielt hierbei irgendwie nicht mit. Von daher habe ich die Service-Datei noch einmal bearbeitet und Zeile 10 wie folgt erweitert.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">ExecStop=/usr/bin/netctl restore ; /usr/bin/systemctl restart openvpn@vpn.service</code>
</pre>

Somit wird erst das Profil mit netctl wieder aktviert und danach die OpenVPN-Verbindung neu gestartet.
