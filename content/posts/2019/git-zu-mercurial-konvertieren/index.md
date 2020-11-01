---
title: Git zu Mercurial konvertieren
date: 2019-05-04T01:45:03+0200
categories:
- OSBN
- Allgemein
tags:
- Git
- Konvertieren
- Mercurial
slug: git-zu-mercurial-konvertieren
---
Oft kommt es vor, dass jemand von einer Versionsverwaltung zu Git wechselt. Ab und zu kommt es aber auch vor, dass jemand von Git auf eine andere Lösung wechseln will. Kürzlich hatte ich solch eine Anfrage. Gewünscht war Mercurial.

Das betreffende Git-Repository war noch recht frisch aber es gab bereits Commits im niedrigen dreistelligen Bereich. Zu viele um diese in Mercurial manuell anzulegen.

Was aber gar nicht nötig ist. Mercurial bietet die Möglichkeit der Konvertierung an.

Nehmen wir einmal an im Home-Verzeichnis gibt es das Verzeichnis repository. In diesem befindet sich das Verzeichnis blog.git in welchem das Git-Repository vorhanden ist. 

Als erstes erzeugt man im Verzeichnis repository das Unterverzeichnis blog.hg und welchselt in dieses. Dort erzeugt man dann mittels "hg init" ein Mercurial-Repository. Hierbei wird das Verzeichnis .hg erstellt. In diesem erzeugt man die Datei hgrc mit folgendem Inhalt.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[extensions]
hgext.convert=
</code>
</pre>

Hiermit aktiviert man die Erweiterung mit der man die Konvertierung vornehmen kann.

Nun führt man im Verzeichnis blog.hg folgenden Befehl aus.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">hg convert --datesort ~/repository/blog.git ~/repository/blog.hg
</code>
</pre>

Das ganze dauert dann etwas. Aber wenn alles geklappt hat, sollte man ein Mercurial-Repository mit allen Commits, Dateien usw. wie im Git-Repository erhalten. Sieht man sich das Verzeichnis blog.hg an, sieht man allerdings weiterhin nur das Unterverzeichnis .hg. Das Problem behebt man in dem man den Befehl "hg update" ausführt. Sieht man sich danach das Verzeichnis blog.hg an sieht man auch die ganzen Dateien die man ursprünglich zum Git-Repository hinzugefügt hat.