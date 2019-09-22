---
title: Borg-Repository auf rsync.net komplett prüfen
date: 2019-09-22T16:17:26+0200
categories:
- OSBN
- Linux
tags:
- Borg
- Rsync.net
slug: borg-repository-auf-rsyncnet-komplett-pruefen
---
Für meine "Offside-Backups" benutze ich [Borg](https://www.borgbackup.org/) und [rsync.net](https://www.rsync.net/products/borg.html). Heute wollte ich meine bei rsync.net gespeicherten Datensicherungen einmal komplett überprüfen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">borg check -v --verify-data XXXXX@ch-s010.rsync.net:MeinRepository
</code>
</pre>

Leider bricht der Befehl schlussendlich immer mit der Fehlermeldung "Borg server is too old for scan. Required version 1.1.0b3" ab. Scheinbar verwendet rsync.net von Haus aus eine ältere Version von Borg. Auf der Internetseite kann man aber nachlesen, dass Version 0.29 und 1.x unterstützt werden. Also sollte es doch möglich sein, die aktuelle Version 1.x zu nutzen. Wie so oft hilft RTFM weiter. Es gibt die Variable BORG_REMOTE_PATH. Mit dieser kann man angeben welche Version von Borg auf dem Server verwendet werden soll. Im Fall von rsync.net muss man den bereits genannten Befehl wie folgt ändern, damit man Version 1.x von Borg verwendet.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">borg check -v --verify-data --remote-path=/usr/local/bin/borg1/borg1  XXXXX@ch-s010.rsync.net:MeinRepository
</code>
</pre>

Anstelle den Parameter --remote-path= zu verwenden, kann man das ganze auch allgemeiner mit "export BORG_REMOTE_PATH=/usr/local/bin/borg1/borg1" angeben. Für Scripte dürfte das die bessere Lösung darstellen.

Vor der Nutzung von --verify-data muss ich abschließend aber noch warnen. Hierbei wird sozusagen alles auf Herz und Nieren geprüft. Und das dauert. In dem Repository das ich für den Test verwendet habe, sind nur knapp 3 GB Daten vorhanden. Bis alles getestet worden ist, sind einige Stunden vergangen. Für allgemeine Prüfungen sollte man daher [andere Einstellungen](https://borgbackup.readthedocs.io/en/stable/usage/check.html) wählen.