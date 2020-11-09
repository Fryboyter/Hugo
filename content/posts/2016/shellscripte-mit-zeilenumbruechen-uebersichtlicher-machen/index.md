---
title: Shellscripte mit Zeilenumbrüchen übersichtlicher machen
date: 2016-04-17T22:18:00+0100
categories:
- Linux
- OSBN
tags:
- Shellscript
- Zeilenumbrüche
slug: shellscripte-mit-zeilenumbruechen-uebersichtlicher-machen
---
Ab und zu werden einzelne Zeilen in einem Shellscript recht lang. Oft zu lang um übersichtlich zu bleiben. Sichert man beispielsweise mit Borg mehrere Verzeichnisse / Dateien kommt z. B. folgendes dabei heraus.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">borg create /pfad/zum/repository/::Montag /home/benutzer/verzeichnis1 /home/benutzer/verzeichnis2 /home/benutzer/verzeichnis3 /home/benutzer/verzeichnis4 /home/benutzer/verzeichnis5 /home/benutzer/verzeichnis6</code></pre>


Übersichtlich ist anders. Also einfach mal ein paar Zeilenumbrüche einbauen?

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">borg create /pfad/zum/repository/::Montag
/home/benutzer/verzeichnis1
/home/benutzer/verzeichnis2
/home/benutzer/verzeichnis3
...</code>
</pre>

Sieht doch schon mal nicht schlecht aus. Mehr aber auch nicht. Denn funktionieren wird das nun nicht mehr, da jede Zeile für sich verarbeitet wird. Das Problem kann man aber recht einfach umgehen. Man packt einfach, von der letzten Zeile abgesehen, einen Backslash an die Ende jeder Zeile.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">borg create /pfad/zum/repository::Monat \
/home/benutzer/verzeichnis1 \
/home/benutzer/verzeichnis2 \
/home/benutzer/verzeichnis3 \
/home/benutzer/verzeichnis4 \
/home/benutzer/verzeichnis5 \
/home/benutzer/verzeichnis6</code>
</pre>

So werden die Zeilenumbrüche ignoriert und der Befehl wird abgearbeitet wie wenn alles in einer Zeile stehen würde.
