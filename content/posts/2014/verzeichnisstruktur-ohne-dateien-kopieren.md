---
title: Verzeichnisstruktur ohne Dateien kopieren
date: 2014-09-07T12:51:00+0100
categories:
- Linux
- OSBN
tags:
- Verzeichnis
- Struktur
- Kopieren
slug: verzeichnisstruktur-ohne-dateien-kopieren
---
Folgendes bekam ich die Tage als Aufgabenstellung. Eine Bekannte von mir hat auf einer Festplatte ein Hauptverzeichnis. Darin enthalten sind Unterverzeichnisse. In diesen sind ebenfalls Unterverzeichnisse usw. In manchen Verzeichnissen liegen Dateien in manchen nicht. Gewünscht war nun, die ganze Verzeichnisstruktur exklusive der Dateien in ein neues Hauptverzeichnis auf einer anderen Platte zu packenn. Das ganze möglichst automatisch, da ein erster manueller Versuch wohl frustriert aufgegeben wurde (sehr viele Verzeichniss und viele Dateien).

Gelöst habe ich ganze wie folgt (mit der Konsole war ich bereits auf dem betreffenden Mountpoint der Festplatte mit den Verzeichnissen inkl. der Dateien).

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">cd Hauptverzeichnis 
find . -type d -exec mkdir -p /mountpoint_der_neuen_platte/Hauptverzeichnis{} ';'
</code>
</pre>

Und schon wurde auf der neuen Platte ein Hauptverzeichnis mit den ganzen Unterverzeichnissen exklusive der Dateien erstellt.
