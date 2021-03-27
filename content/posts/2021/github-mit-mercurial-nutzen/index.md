---
title: Github mit Mercurial nutzen
date: 2021-03-27T14:35:02+0100
description: Anleitung wie man mittels des Plugins hg-git ein Git-Repository mit der Versionsverwaltung Mercurial nutzen kann
categories:
- OSBN
- Allgemein
tags:
- Github
- Mercurial
- Hg-git
slug: github-mit-mercurial-nutzen
---
Vor ein oder zwei Wochen habe ich mir eines meiner Git-Repository zerlegt. Da mich die Lösung viel Zeit, zu viele Nerven und zwei Commits gekostet hat, bin ich nun wieder bei [Mercurial](https://www.mercurial-scm.org) gelandet. Dieses Werkzeug mag zwar nicht so mächtig wie Git sein, die Fehlermeldungen sowie die Dokumentation sind meiner Meinung nach viel besser verständlich.

Allerdings will ich auch weiterhin Github aufgrund dessen weiter Verbreitung nutzen. Sei es nun um dort selbst etwas zu veröffentlichen oder um mich an Projekten Dritter zu beteiligen. Mercurial bietet hierfür ein Plugin, dass sich [hg-git](https://foss.heptapod.net/mercurial/hg-git) nennt. Damit kann man ein Git-Repository herunterladen und es wird lokal automatisch in ein Mercurial-Repository umgewandelt. Nimmt man nun Änderungen vor, werden diese dann vor dem Hochladen in ein Git-Repository so geändert, dass sie mit Git kompatibel sind. Die Einrichtung von hg-git ist zudem ziemlich einfach.

Ich gehe bei folgender Anleitung davon aus, dass sowohl Mercurial als auch python-dulwich auf dem Rechner installiert ist und das im Home-Verzeichnis das Verzeichnis Projekte existiert. Dem Verzeichnis kann man natürlich einen anderen Namen geben.

Zuerst wechselt man im Terminal Emulator seiner Wahl in das Verzeichnis Projekte und läd dort die Dateien von hg-git herunter.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cd ~/Projekte
hg clone https://foss.heptapod.net/mercurial/hg-git hg-git</code>
</pre>

Alternativ kann man hg-git auch über die Paketverwaltung seiner Distribution installieren. 

Als nächstes erweitert man die Datei .hgrc im Home-Verzeichnis um folgenden Inhalt. Falls die Datei noch nicht vorhanden ist, einfach anlegen und die drei Zeilen eintragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[extensions]
hgext.bookmarks =
hggit = ~/Projekte/hg-git/hggit</code>
</pre>

Zeile zwei aktiviert das Plugin Bookmarks das in diesem Fall Branches simuliert. Zeile drei aktiviert das eben heruntergeladene Plugin hg-git.

Im Verzeichnis Projekte laden wir nun mit folgendem Befehl ein Git-Repository herunter (die Github-Adresse sowie das Zielverzeichnis fryboyter.git bitte entsprechend an die eigenen Gegebenheiten anpassen).

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">hg clone git@github.com:Fryboyter/Hugo.git fryboyter.hg</code>
</pre>

Da hierbei von Git zu Merurial umgewandelt wird, kann dies je nach Größe des Repository etwas dauern.

Als nächstes wechselt man in das Verzeichnis in dem das nun erstellete Mercurial-Respository liegt. In diesem Beispiel also fryboyter.hg. Dort führt man abschließend noch den Befehl <mark>hg bookmark -f main</mark> aus. Anstelle von main muss man die Bezeichnung des Haupt-Branch angeben. Ansonsten erkennt Mercurial bei einem Push keine Änderungen.

Nun sollte alles funktionieren. Bei meinen Tests konnte ich zumindest problemlos von Github pullen und zu Github pushen. Mehr brauche ich in meinem Fall eigentlich auch nicht. Was mir bei der ganzen Aktion aufgefallen ist, dass das lokale Mercurial-Repository weniger als 30 MB groß ist. Das lokale Git-Repository hingegen belegt etwas mehr als 60 MB. Davon geht die Welt jetzt nicht unter aber es ist trotzdem ein interessantes Detail.
