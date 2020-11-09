---
title: Aktuellste Programmversion per Script von Github laden
date: 2017-08-17T00:04:57+0100
categories:
- Linux
- OSBN
tags:
- Github
- Download
- Aktuelle Version
slug: aktuellste-programmversion-per-script-von-github-laden
---
Einige Projekte auf Github bieten Nightly Builds an. Also Programmversionen die in der Regel über Nacht und automatisiert erstellt werden. Die Frage ist nur, wie kann man sich diese herunterladen wenn sich der Dateiname ändert?


Nehmen wir als Beispiel mal den Editor micro. Bei diesem Projekt werden Nightly Builds für x Architekturen angeboten. Für ARM ist zum Beispiel gerade die Datei "micro-1.3.2-10-linux-arm.tar.gz" aktuell. Morgen vielleicht "micro-1.3.2-11-linux-arm.tar.gz" oder "micro-1.3.2-14-linux-arm.tar.gz". Hier sehe ich zwei Lösungen. Entweder man läd die Datei manuell herunter oder man automatisiert den Download. Ich bevorzuge eindeutig Möglichkeit Nummer 2. Allerdings war mal wieder die Lösung das Problem. Mittels curl, jq und wget konnte ich das Problem aber lösen. Folgendes Script ist dabei entstanden.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/sh
arch=linux-arm
link=$(curl -s https://api.github.com/repos/zyedidia/micro/releases/tags/nightly | jq -r ".assets[] | select(.name | test(\"${arch}\")) |  .browser_download_url")
wget $link</code>
</pre>

In Zeile zwei gibt man die gewünschte Architektur an. Eine Übersicht der vorhandenen Möglichkeiten findet man unter [https://github.com/zyedidia/micro/releases](https://github.com/zyedidia/micro/releases).

Zeile drei greift auf die API von Github zu und mittels jq wird der gewünschte Downloadlink erstellt.

Zeile 4 läd die gewünschte Datei herunter.

Vermutlich gibt es einfachere und bessere Lösungen. Aber das obige Script funktioniert und reicht mir für den Hausgebrauch.
