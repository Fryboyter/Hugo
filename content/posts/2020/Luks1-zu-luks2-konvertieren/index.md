---
title: Luks1 zu luks2 konvertieren
date: 2020-06-16T18:57:32+0200
categories:
- OSBN
- Linux
tags:
- Cryptsetup  
- Luks
slug: luks1-zu-luks2-konvertieren
---
Meine Rechner sind mittels cryptsetup und luks verschlüsselt. Bei meinem Notebook habe ich das schon vor Jahren gemacht, so dass hier immer noch luks in Version 1 verwendet wird. Bei luks in Version 2 wird allerdings [Argon2](https://de.wikipedia.org/wiki/Argon2) verwendet, was einen Angriff mittels Brute Force erheblich erschwert. 

Wie kann man nun auf Version 2 wechseln ohne die Partitionen neu verschlüsseln zu müssen?

Als erstes sollte man überprüfen ob man nicht schon Version 2 nutzt. Dies erreicht man mit folgendem Befehl:

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cryptsetup luksDump /dev/sda2 | grep -A1 "^LUKS"</code>
</pre>

Anstelle von /dev/sda2 muss man seine verschlüsselte Partition angeben. Dies gilt auch für alle weiteren Befehle. Wird hiermit Version: 2 angezeigt kann man sich weitere Schritte sparen. Wenn Version: 1 angezeigt wird, geht es weiter und man sollte man als erstes den Header sichern. Denn geht etwas schief kommt man nicht wieder an seine Daten. Zum Sichern führt führt man folgenden Befehl aus:

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cryptsetup luksHeaderBackup /dev/sda2 --header-backup-file sicherung.dat</code>
</pre>

Die Datei sicherung.dat kopiert man anschließend auf einen USB-Stick oder auf einen anderen Rechner, da dies neben der Datensicherung (die natürlich jeder regelmäßig erstellt...) unsere Versicherung ist.

Nun geht es ans Eingemachte. Der folgende Befehl konvertiert luks 1 zu luks 2.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cryptsetup convert /dev/sda2 --type luks2</code>
</pre>

Nun nutzt die verschlüsselte Partition luks 2. Allerdings wird für das Passwort erst einmal nicht Argon2 verwendet sondern das was man ursprünglich angegeben hat. In meinem Fall pbkdf2. Also ist noch ein Befehl nötig um dies zu ändern.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cryptsetup luksChangeKey /dev/sda2 --pbkdf argon2id</code>
</pre>

Hierbei wird man aufgefordert sein bisheriges und ein neues Passwort einzugeben. Es ist aber auch möglich als neues Passwort erneut sein altes Passwort einzugeben.

Ein abschließender Test mittels <mark>cryptsetup luksDump /dev/sda2</mark> sollte nun zum einen Version: 2 als auch die Verwendung von Argon2id anzeigen. Nutzt man mehrere Schlüssel, muss man den Befehl mit luksChangeKey für jeden Schlüssel wiederholen. 

Funktioniert nach einem Neustart des Rechners alles wie gewohnt, sollte man vorsichtshalber noch die Header-Sicherung löschen.
