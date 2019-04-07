---
title: Verzeichnis mit systemd überwachen
date: 2015-09-02T21:30:00+0100
categories:
- Linux
- OSBN
tags:
- Systemd
- Verzeichnis
- Überwachen
slug: verzeichnis-mit-systemd-ueberwachen
---
Heute bekam ich folgende Anfrage (hier abgewandelt, da der genaue Vorgang intern bleiben soll). Wenn in einem Verzeichnis eine Avi-Datei gespeichert wird soll diese automatisch in eine Mkv-Datei (libtheora und libvorbis) umgewandelt und verschoben werden.

Als erstes habe ich unter /home/video/ das Verzeichnis videos und Verzeichnis videos2 erstellt. Als nächstes habe ich im gleichen Homeverzeichnis folgendes Shellscript erstellt:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
cd /home/video/videos/ 
for i in *.avi; do
ffmpeg -i "$i" -vcodec libtheora -acodec libvorbis "${i%.*}.mkv" 
done
mv *.mkv /home/video/videos2/
rm *.avi</code>
</pre>

Das Shellscript wechselt erst in das eben erstellte Verzeichnis videos. Dort sucht es nach vorhandenen Dateien mit der Endung .avi und wandelt diese in eine Mkv-Datei mit libtheora und Libvorbis um. Danach werden die Mkv-Dateien in das Verzeichnis videos2 verschoben und die vorhandenen Avi-Datei gelöscht.

Als nächstes habe ich mir Root-Rechte verschafft und mit diesen unter /etc/systemd/system die Datei convert.service mit folgendem Inhalt angelegt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Videos in ~/home/video/video automatisch konvertieren

[Service]
Type=oneshot
ExecStart=/home/video/convert.sh</code>
</pre>

Hier wird im Grunde genommen nur angegeben, dass das eben erstellte Shellscript convert.sh ausgeführt wird.

Im gleichen Verzeichnis habe ich nun noch die Datei convert.path angelegt und mit folgendem Inhalt befüllt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Startet convert.service wenn eine Datei in /home/video/video$ 

[Path]
PathModified=/home/video/videos/ 

[Install]
WantedBy=multi-user.target</code>
</pre>

Hier ist der Abschnitt Path der wichtige Teil. Sobald im Verzeichnis /home/video/videos etwas geändert wird (wie eben dass dort eine Avi-Datei abgespeichert wird) wird das in der Service-Datei genannte Shellscript ausgeführt. Anstelle von PathModified gibt es noch PathExists=, PathExistsGlob=, PathChanged=, und DirectoryNotEmpty=. Diese werden unter man systemd.path oder [hier](http://www.freedesktop.org/software/systemd/man/systemd.path.html) online genauer erklärt.

Nun habe ich mittels systemctl start convert.path das ganze einmalig gestartet. Das es nach einem Testlauf kein Probleme gegeben hat, habe ich diese Automatisierung mittels systemctl enable convert.path scharf geschaltet so dass der Spaß auch einen Neustart des Systems überlebt.
