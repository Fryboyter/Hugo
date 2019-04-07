---
title: Fryboyter wird nun mit Hugo erzeugt
date: 2019-04-07T20:44:00+0100
categories:
- OSBN
- Allgemein
tags:
- Fryboyter
- Hugo
- Git
slug: fryboyter-wird-nun-mit-hugo-erzeugt
---
Bisher habe ich für fryboyter.de das CMS [Bolt](https://bolt.cm/) verwendet. Im Grunde bin ich damit auch zufrieden. Aber irgendwie habe ich in letzter Zeit immer weniger Lust die Updates zu installieren.

Daher habe ich mir in den letzten Wochen diverse Tools angesehen, mit denen man statische Webseiten erstellen kann. Man braucht also kein PHP, keine Datenbank usw. Somit entfällt auch das nervige Updaten der Seite.

Schlussendlich bin ich bei [Hugo](https://gohugo.io/) gelandet. Das hat im Grunde zwei Gründe. Zum einen besteht Hugo nur aus einer Datei und zum anderen werden die statischen Seiten sehr schnell erzeugt.

Was mich aber etwas beschäftigt hat war, wie ich die Seite bei neuen Artikeln möglichst einfach erzeugen und auf den Webspace hochladen kann. 

Im [Lab](https://lab.uberspace.de/guide_hugo.html) von Uberspace gibt es inzwischen eine Anleitung wie man Hugo installiert. Hierbei läuft Hugo als Dienst im Hintergrund und erzeugt die Seite neu sobald sich etwas geändert hat. Was aber zur Folge hat, dass ich mich wieder zeitnah um eventuelle Updates kümmern muss. Besser wäre es, wenn Hugo nur zum Erzeugen der Seite gestartet und danach wieder beendet wird. Das einfachste wäre es, sich per SSH mit dem Webspace zu verbinden, den neuen Artikel zu erstellen und dann Hugo manuell auszuführen. Einfach? Ja. Umständlich? Auf jeden Fall. Also kommt es auch nicht in Frage.

Die Lösung lautet, wie so oft, Git. Als erstes legt man auf dem Webspace außerhalb des Document Root ein Verzeichnis an. In diesem erzeugt man mittels "git init --bare" ein sogenannte Bare-Respository. Dies hat, im Gegensatz zu einem normalen Respository keinen Working Tree. Schaut man sich nun das Verzeichnis noch einmal an, findet man dort das Unterverzeichnis "hooks". Mit diesen Hooks lassen sich bestimmte Dinge automatisieren. Zum Beispiel lassen sich Befehle ausführen wenn das Repository neue Daten erhalten hat. Hierfür legt man im Verzeichnis "hooks" die Datei post-receive an und befüllt diese beispielsweise wie folgt und macht diese dann noch ausführbar.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">GIT_REPO=$HOME/repository/fryboyter.git
TMP_GIT_CLONE=$HOME/tmp/git/fryboyter
PUBLIC_WWW=/var/www/virtual/$USER/html/fryboyter
git clone $GIT_REPO $TMP_GIT_CLONE
~/bin/hugo -s $TMP_GIT_CLONE --cleanDestinationDir -d $PUBLIC_WWW
rm -Rf $TMP_GIT_CLONE
exit
</code>
</pre>

Hiermit wird der Inhalt des Repository in ein temporäres Verzeichnis geklont. Danach löscht Hugo die bereits veröffentlichte Internetseite und erstellt diese neu. Danach wird das temporäre Verzeichnis gelöscht.

Was jetzt noch fehlt, sind die Daten mit denen man die Internetseite erzeugt. Diese erzeugt man auf dem eignene Rechner. Wenn dies erledigt ist, wechselt man in das betreffende Verzeichnis und führt folgende Befehle aus.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">git init
git add .
git commit -m "Beschreibung des Commit"
</code>
</pre>

Hiermit erstellt man ein lokales Repository, fügt alle Dateien des Verzeichnis hinzu und erstellt einen Commit. Läde man das ganze mittels "git push $adresse_des_repository" hoch wird automatisch die Datei post-receive ausgeführt und die Internetseite wird autoamtisch erzeugt. Um zukünftig die Seite zu aktualisieren, erzeugt / ändert man die betreffende Datei im lokalen Repository, erstellt einen neuen Commit und läd die Änderungen mittels git push hoch.