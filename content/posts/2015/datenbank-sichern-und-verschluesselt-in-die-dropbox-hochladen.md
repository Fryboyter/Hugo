---
title: Datenbank sichern und verschlüsselt in die Dropbox hochladen
date: 2015-10-10T16:49:00+0100
categories:
- Linux
- OSBN
tags:
- MySQL
- Datenbank
- Backup
- Dropbox
slug: datenbank-sichern-und-verschluesselt-in-die-dropbox-hochladen
---
Ungesicherte Daten sind unwichtige Daten. Daher sollte man sich gut überlegen wie und vor allem wohin man seine wichtigen Daten sichert. Bei vielen Betreibern ist zum Beispiel die Datenbank absolut wichtig, da dort die Artikel und Kommentare eines Blogs gespeichert sind. Da eine Datensicherung prinzipiell auf einem anderen Speichermedium zu erfolgen hat als die Originaldaten liegen, habe ich mir überlegt, ob man hierfür nicht eine [Dropbox](https://www.dropbox.com) nutzen könnte. Man kann.

Als erstes läd man sich von [https://github.com/andreafabrizi/Dropbox-Uploader](https://github.com/andreafabrizi/Dropbox-Uploader) die Shellscripte herunter und speichert diese in einem Verzeichnis auf den Server. Hier sollte man nach Möglichkeit das Verzeichnis außerhalb des Document Root anlegen.

Nun macht man mittels

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">chmod +x dropbox_uploader.sh</code>
</pre>

das Shellscript ausführbar und startet es. Beim ersten Start wird hierbei der Konfigurationsvorgang ausgeführt. Diesem folgt man dann entsprechend (eine Dropbox muss bereits vorhanden sein). Da man hier eigentlich nichts falsch machen kann, gehe ich an dieser Stelle nicht näher darauf ein. Falls doch Fragen aufkommen sollten, meldet euch einfach. Nachdem der Uploader konfiguriert wurde, kann man diesen schon einmal testen indem man mit <code>touch test.txt</code> eine Datei erstellt und diese dann mittels

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">./dropbox_uploader.sh upload test.txt .</code>
</pre>

in die Dropbox hochläd.

Nun erstellt man im gleichen Verzeichnis in dem das Shellscript liegt ein weiteres. Beispielsweise backup.sh. Dies füllt man dann wie folgt:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
set -e DAY=`/bin/date +%Y%m%d`
PASSPHRASE='a=Fr#M?w\\+.Qg3T.qD)x'
mysqldump -u benutzername -p'4567' datenbankname | gzip -9 &gt; /home/benutzername/Dropbox-Uploader/$DAY.sql.gz
gpg --batch --cipher-algo AES256 --passphrase=$PASSPHRASE -c /home/benutzername/Dropbox-Uploader/$DAY.sql.gz
cd /home/benutzername/Dropbox-Uploader/ 
./dropbox_uploader.sh upload "$DAY.sql.gz.gpg" . 
rm /home/benutzername/Dropbox-Uploader/$DAY.sql.gz 
rm /home/benutzername/Dropbox-Uploader/$DAY.sql.gz.gpg</code>
</pre>

Das ganze Script ist relativ schnell erklärt. Erst wird ein Dump der Datenbank "datenbankname" erstellt und gepackt. Hierbei wird der Dateiname wie in Zeile drei definiert erstellt (Jahr/Tag/Monat). Als nächstes wird das so erstellte Archiv mittels gpg und dem in Zeile vier hinterlegtem Passwort verschlüsselt. Danach wird die verschlüsselte Datei in die Dropbox hochgeladen. Abschließend wird sowohl die verschlüsselte als auch die unverschlüsselte Datei vom Server gelöscht.

Nun legt man sich am besten noch einen Cronjob an mit dem dann das eben erstelle Script regelmäßig ausgeführt wird und somit die Datenbank automatisch gesichert wird.
