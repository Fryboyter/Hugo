---
title: Git - Nicht übergebene Änderungen rückgängig machen
date: 2020-07-06T18:05:41+0200
categories:
- OSBN
- Allgemein
tags:
- Git  
- Restore
slug: git-nicht-uebergebene-aenderungen-rueckgaengig-machen
---
Gestern habe ich begonnen Änderungen in einem Repository auf meinem Notebook durchzuführen. Die bisherigen Änderungen habe ich allerdings noch nicht mit einem Commit gepflegt.

Da ich die Änderung heute schnellstmöglich einpflegen wollte, habe ich die Änderungen kurzerhand komplett auf einem anderen Rechner durchgeführt und einen entsprechenden Commit erstellt und diesen hochgeladen.

Eben wollte ich die Kopie des Repository auf meinem Notebook mit <mark>git pull</mark> aktualisieren. Das Ergebnis war allerdings folgende Fehlermeldung.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">git pull
error: Pull mit Rebase nicht m&ouml;glich: Sie haben &Auml;nderungen, die nicht zum Commit vorgemerkt sind.
error: Bitte committen Sie die &Auml;nderungen oder benutzen Sie &quot;stash&quot;.</code>
</pre>

Da ich ziemlich viel getestet hatte, habe ich mir erst einmal mit <mark>git status</mark> angesehen um welche Dateien es überhaupt geht. Eine der Dateien war style.css. Nach etwas Recherche bin ich auf <mark>git restore</mark> gestoßen. Mittels folgendem Befehl habe ich die Änderungen in der Datei style.css kurzerhand rückgängig machen können.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">git restore themes/fryboyter/static/css/style.css</code>
</pre>

Das ganze habe ich dann auch auf die restlichen geänderten Dateien angewand und konnte dann die bereits eingepflegten Änderungen mit <mark>git pull</mark> herunterladen.
