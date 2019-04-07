---
title: Commandlinefu
date: 2012-12-26T13:11:00+0100
categories:
- Linux
- OSBN
tags:
- Shell
- Befehle
- Erklärung
slug: commandlinefu
---
Für die Shell-Fetischisten habe gerade einen recht nützlichen Link ausgegraben.

[Http://www.commandlinefu.com](http://www.commandlinefu.com "http://www.commandlinefu.com") ist eine Sammelstelle für diverse Shell-Befehle inkl. deren Erklärung. Dort findet man relativ leicht nachvollziehbare Befehle wie

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">file -sL /dev/sda4</code>
</pre>


mit denen man beispielsweise das Dateisystem einer Partition herausfinden kann. Aber auch schwerere Geschütze wie

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">ps -eo size,pid,user,command --sort -size |awk '{hr[1024**2]="GB";hr[1024]="MB";for (x=1024**3; x&gt;=1024; x=1024){if ($1&gt;=x){printf ("%-6.2f %s ", $1/x, hr[x]);break}}}{printf ("%-6s %-10s ", $2, $3)}{for (x=4;x&lt;=NF;x++){printf ("%s ",$x)} print ("/n")}'</code>
</pre>

mit denen man sich in einer übersichtlichen Weise anzeigen lassen kann, welche Speichermenge sich die Prozesse geschnappt haben. In der rechten Spalten der Seite gibt es diverse Tags wie bzip2, chmod, oder screen. Damit lässt sich das ganze schon einmal eingrenzen, wenn man sich nur Befehle für einen bestimmten Befehl/Bereich anzeigen lassen will. Eine Suchfunktion ist ebenfalls vorhanden, wenn man etwas genauer suchen will.
