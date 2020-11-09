---
title: Webanwendung mit git aktualisieren und Änderungen behalten
date: 2017-11-26T16:21:15+0100
categories:
- Linux
- OSBN
tags:
- Git
- Stash
slug: webanwendung-mit-git-aktualisieren-und-aenderungen-behalten
---
Manche meiner Webanwedungen aktualisiere ich mittels git. Bei meiner Instanz von [Searx](https://github.com/asciimoo/searx) bekomme ich allerdings eine Fehlermeldung, wenn ich git pull origin master ausführe, weil ich lokal einige geänderte Dateien habe. In meinem Fall sind das Konfigurationsdateien wie settings.yml.

Da ich ehrlich gesagt keine Lust habe, hier jedes mal die Änderungen wieder auf meinem Webspace einzupflegen habe ich mal geschaut, was bei git so alles möglich ist. Bei git stash bin ich fündig geworden. Hiermit werden Änderungen an den lokalen Dateien quasi gesichert und können nach einem Update der lokalen Dateien wieder eingespielt werden.

Aktuell läuft daher die Aktualisierung von Searx daher wie folgt ab.

<pre class="line-numbers language-git" style="white-space:pre-wrap;">
<code class="language-git">git stash
git pull origin master
git stash pop</code>
</pre>

Mit dem ersten Befehl lege ich mir quasi eine Kopie der Änderungen an. Mit dem zweiten Befehl spiele ich alle Änderungen seitens der Entwickler ein. Der letzte Befehl spielt dann meine Änderungen in die aktualisierten lokalen Dateien ein und löscht die Kopie wieder.
