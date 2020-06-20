---
title: Sddm - Nur auf einem Monitor anmelden
date: 2020-02-29T19:27:37+0100
categories:
- OSBN
- Linux
tags:
- Sddm 
slug: sddm-nur-auf-einem-Monitor-anmelden
---
Achtung dieser Artikel löst ein Luxusproblem! An meinem Hauptrechner sind zwei Monitore angeschlossen und als Display Manager nutze ich [SDDM](https://github.com/sddm/sddm). SDDM hat bei mehreren Monitoren die Angewohnheit, auf allen Monitoren das Gleiche angezeigt, so dass man sich prinzipiell über jeden Monitor anmelden kann. Mich nervt das aber irgendwie; zumal ich mich immer an dem Monitor anmelde der direkt vor mir steht. Wie gesagt, ein Luxusproblem.

SDDM sieht es selbst aktuell nicht vor, dass die Eingabemaske nur auf einem Monitor erscheint. Also ist wieder Handarbeit nötig. Hierfür benötigt man das Tool xrandr. Unter Arch hat das Paket die Bezeichnung xorg-xrandr.

Mittels <mark>xrandr | grep ' connected'</mark> lässt man sich als erstes die angeschlossenen Monitore anzeigen und sucht sich denjenigen heraus, den man unter SDDM **nicht** nutzen will. Bei mir ist das relativ leicht, da dieser die geringere Auflösung hat. Nehmen wir einmal folgendes Beispiel

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">(Standardeingabe):20:DP-4 connected 1920x1200+0+0 (normal left inverted right x axis y axis) 518mm x 324mm
</code>
</pre>

Der Monitor ist in diesem Fall also über den Anschluss DP-4 angeschlossen. Nun erstellt man das Script /usr/share/sddm/scripts/Xsetup und trägt folgendes ein.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/sh
xrandr --output DP-4 --off
</code>
</pre>

DP-4 muss man natürlich an die eigenen Gegebenheiten anpassen.

Nun trägt man noch folgendes in die Datei /etc/sddm.conf ein (wenn die Datei nicht vorhanden ist, einfach anlegen).

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[XDisplay]
DisplayCommand=/usr/share/sddm/scripts/Xsetup
</code>
</pre>

Bootet man den Rechner nun neu, sollte der im Script genannte Monitor bei Einloggen nichts mehr anzeigen. Sobald man sich angemeldet hat, ist der Monitor aber wieder automatisch nutzbar.
