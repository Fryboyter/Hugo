---
title: Gesprächigkeit eines systemd-Service einstellen
date: 2015-02-16T21:44:00+0100
categories:
- Linux
- OSBN
tags:
- Gesprächigkeit
- Service
- Systemd
slug: gespraechigkeit-eines-systemd-service-einstellen
---
Vor ca. zwei Wochen habe ich für [ngb.to](https://ngb.to "ngb.to") einen Quake-3-Arena-Server auf auf Basis von ioquake aufgesetzt. Als Distribution habe ich Arch Linux gewählt. Nachdem alles installiert war, wollte ich den Q3A-Server nach dem Booten und nach einem eventuelle Absturz neu starten lassen. Mittels eines systemd-Service kein Problem. Nur ist Q3A an sich eine Quasselstrippe und müllt die Logdateien gnadenlos zu. Vor allem wenn gezockt wird. Hier bin ich mir nicht sicher wie lange das mit der, im Raspberry Pi verbauten, Speicherkarte gut geht. Daher musste ein Weg her um Q3A zum Schweigen zu bringen.

Nach einer kurzen Suche in der Dokumentation von systemd wurde ich fündig. Hier hilft StandardOutput= weiter. Hierüber kann man die Standardausgabe eines Service definieren. Zur Auswahl stehen inherit, null, tty, journal, syslog, kmsg, journal+console, syslog+console, kmsg+console sowie socket. Da mich die Standardausgabe (X hast joined usw.) nun wirklich nicht interessiert, war ich gnadenlos und habe null gewählt. Somit werden die ganzen Ausgaben direkt gemülleimert und das Journal und somit auch die Speicherkarte werden geschont. Herausgekommen ist dann folgender Service.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Startet ioquake3-Server

[Service]
User=q3a
ExecStart=/pfad/zum/Startscript/q3a.sh
StandardOutput=null
Restart=always

[Install]
WantedBy=multi-user.target</code>
</pre>

Wenn man will kann man auch noch StandardError= für eventuell auftretende Fehler definieren. Hier gelten wieder oben genannte Möglichkeiten. Gibt man dies nicht direkt in der Service-Datei an, wird der Standard inherit verwendet.
