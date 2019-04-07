---
title: Man pages - Too long didn''t read
date: 2017-10-30T10:47:04+0100
categories:
- Linux
- OSBN
tags:
- Man pages
- Tldr
slug: man-pages-too-long-didn-t-read
---
Manche der Man Pages sind rech lang und teilweise inhaltlich recht kompliziert. Das nervt vor allem, wenn man nur mal eben die Grundfunktionen eines Befehls nachschlagen will. Wie zum Beispiel das Entpacken eines Tar-Archives.

Hier ist das Projekt &gt;tldr _ (was für ein Name) eine nette Idee. Unter https://tldr.ostera.io kann man einfach den gewünschten Befehl eingeben und erhält Beispiele für die grundlegenden Funktionen. Bei tar wird beispielsweise folgendes ausgespuckt.

<pre>
<code>Create an archive from files:
tar cf {{target.tar}} {{file1 file2 file3}}

Create a gzipped archive:
tar czf {{target.tar.gz}} {{file1 file2 file3}}

Extract an archive in a target folder:
tar xf {{source.tar}} -C {{folder}}

Extract a gzipped archive in the current directory:
tar xzf {{source.tar.gz}}

Extract a bzipped archive in the current directory:
tar xjf {{source.tar.bz2}}

Create a compressed archive, using archive suffix to determine the compression program:
tar caf {{target.tar.xz}} {{file1 file2 file3}}

List the contents of a tar file:
tar tvf {{source.tar}}</code>
</pre>

Sollte man einen Fehler finden, lassen sich die Seiten auf Github recht schnell bearbeiten. Was nach ein paar Test allerdings auffällt ist, dass hier noch viele Befehle wie whereis fehlen. Im AUR von Arch steht das ganze auch zum Installieren auf dem eigenen Rechner zur Verfügung.
