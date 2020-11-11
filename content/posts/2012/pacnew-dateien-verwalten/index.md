---
title: Pacnew Dateien verwalten
date: 2012-09-30T04:05:00+0100
categories:
- Linux
- OSBN
tags:
- Pacnew
- Verwalten
- Arch Linu
slug: pacnew-dateien-verwalten
---
Unter Arch Linux werden bestehende Konfigurationsdateien bekanntlich nicht bei Updates der dazu gehörenden Pakete überschrieben. Statt dessen wird eine pacnew-Datei angelegt. Also wenn z. B. die Datei rc.conf bereits vorhanden ist wird im gleichen verzeichnis eine rc.conf.pacnew angelegt. Zum Vergleichen und zusammenführen eventuell vorhandener Änderungen benutze ich ein Script, welches das kleine aber feine Tool [meld](http://meldmerge.org/ "meld") verwendet.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
pacnew=$(find /etc -type f -name "*.pacnew")
# Check if any .pacnew configurations are found
if [[ -z "$pacnew" ]]; then
echo " No configurations to update"
fi
for config in $pacnew; do
# Diff original and new configuration to merge
kdesu meld ${config%\.*} $config &amp;
wait
# Remove .pacnew file?
while true; do
read -p " Delete \""$config\"\"? (Y/n): " Yn
case $Yn in
[Yy]* ) sudo rm "$config\" &amp;&amp; \
echo " Deleted \""$config\"\"."
break ;;
[Nn]* ) break ;;
* ) echo " Answer (Y)es or (n)o.\" ;;
esac
done
done</code>
</pre>

Mit diesem Script wird man nach dem Vergleichen und Zusammenführen gefragt, ob man die jeweilige pacnew-Datei löschen will. Wäre da nicht sudo. Ich habe eine absolute Abneigung gegen sudo. Von daher funktioniert das hier nicht. Tja und da ich es auch nicht einrichten werde, habe ich mir statt dessen ein weiteres Script gebaut, dass nach pacnew-Dateien sucht und diese dann löscht. Das gleiche gilt für pacsave- und pacorig-Dateien. Naja eigentlich nur einen Einzeiler...

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">>find / -type f -name "*.pacnew" -exec rm -i {} \\;</code>
</pre>

Jetzt noch den sudo-Kram im ersten Script entfernt und ich bin einigermaßen zufrieden.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
pnacnew=$(find /etc -type f -name "*.pacnew")
for config in $pacnew; do
kdesu meld ${config%\.*} $config &amp;
wait
done</code>
</pre>
