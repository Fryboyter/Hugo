---
title: Paketverwaltung von Arch Linux auf dem Raspberry Pi beschleunigen
date: 2016-08-11T19:17:00+0100
categories:
- Linux
- OSBN
tags:
- Arch Linux
- Paketverwaltung
slug: paketverwaltung-von-arch-linux-auf-dem-raspberry-pi-beschleunigen
---
Seit längerem stelle ich einen Server für Quake 3 Arena zur Verfügung. Dieser läuft auf einem Raspberry Pi 3 mit ALARM (Arch Linux für ARM). Da dieser jedem zur Verfügung steht, muss ich regelmäßig die Pakete aktualisieren. Hierbei hängt der Updatevorgang in der Regel bei (1 / 3) Updating manpage index... und (2 / 3) Updating the info directory file... für einige Minuten fest.

Um beides schnell abzuwickeln ist der Raspberry Pi einfach zu schwach. Daher habe mir überlegt, brauche ich direkt nach einem Update bzw. einer Installation eines Pakets z. B. einen aktuellen Manpage-Index auf dem Raspberry Pi? Eigentlich nicht. Verantwortlich für die beiden Schritte sind sogenannte Hooks die es seit Pacman 5 gibt. Diese liegen unter /usr/share/libalpm/hooks/. In dem Verzeichnis liegen unter anderem die Dateien man-db.hook und texinfo-install.hook. Laut der Manpage von libalpm lassen sich die Hooks deaktivieren wenn man sie nach /dev/null umleitet. Um nicht an den originalen Hooks Änderungen vorzunehmen, erstellen wir unter /etc/pacman.d erst einmal das Verzeichnis hooks. Alle Hooks die dort vorhanden sind, überschreiben die, die unter /usr/share/libalpm/hooks/ vorhanden sind. Dort erstellen wir dann zwei Symlinks die nach /dev/null zeigen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">ln -s /dev/null /etc/pacman.d/hooks/man-db.hook
ln -s /dev/null /etc/pacman.d/hooks/texinfo-install.hook</code>
</pre>

Installiert oder aktualisiert man nun ein Paket und hat die Debug-Funktion von pacman aktiviert, sollte man folgende Zeilen in der Ausgabe finden und der Vorgang sollte schnell durchlaufen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">debug: skipping overridden hook /usr/share/libalpm/hooks/man-db.hook 
debug: skipping overridden hook /usr/share/libalpm/hooks/texinfo-install.hook</code>
</pre>

So ganz ohne aktuellen Manpage-Index wollte ich dann aber doch nicht sein. Früh morgens findet auf dem Server im Grunde genommen keine Aktivität statt. Dann könnte man beide Hooks ja eigentlich laufen lassen. Lösen kann man das ganze über systemd und den timern. Diese sind in etwa vergleichbar mit den bekannten Cronjobs. Unter /etc/systemd/system/ erstellt man hierfür erst einmal zwei Service- sowie zwei Timer-Dateien mit folgendem Inhalt.

manpage-index.service

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Manpage-Index aktualisieren

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'mkdir -p /var/cache/man; exec mandb --quiet --no-purge'</code>
</pre>

manpage-index.timer

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Manpage-Index täglich aktualisieren

[Timer]
OnCalendar=*-*-* 02:30:00
Persistent=true</code>
</pre>

texinfo-index.service

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Texinfo aktualisieren

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'for f in /usr/share/info/*.gz; do install-info "$f" /usr/share/info/dir 2&gt; /dev/null; done'</code>
</pre>

texinfo-index.timer

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=Run texinfo updater daily
[Timer]
OnCalendar=*-*-* 03:30:00
Persistent=true
</code>
</pre>

Mit systemctl start texinfo-index.timer und systemctl start manpage-index.timer werden die beiden Timer dann noch abschließend aktiviert, so dass diese nun täglich um 2.30 und 3.30 Uhr gestartet werden.
