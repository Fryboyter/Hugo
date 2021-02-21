---
title: Git - Bereits gesendete Commits zusammenfassen
date: 2021-01-08T01:36:51+0100
categories:
- OSBN
tags:
- Git
- Commit
slug: git-bereits-gesendete-commits-zusammenfassen
---
Ich habe an mehreren Dateien in einem Git-Repository jeweils die gleiche Änderung durchgeführt. Hierfür habe ich pro Datei einen Commit erstellt und diese bereits zu Github übermittelt. Ein Commit hätte es in dem Fall auch getan. Wie kann man nun nachträglich die betreffenden Commits zu einem Commit zusammenfassen?

Als erstes führt man im lokalen Arbeitsverzeichnis <mark>git rebase -i HEAD~X</mark> aus. Anstelle von X gibt man die Anzahl der letzten Commits an die man zusammenfassen möchte.

Nun sollte automatisch ein Editor geöffnet werden und in den ersten Zeilen sollte man beispielsweise folgendes vorfinden.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">pick 67426ab Commit-Nachricht
pick 56432tz Commit-Nachricht
pick 45643io Commit-Nachricht</code>
</pre>

Um aus diesen drei Commits einen Commit zu machen ersetzt man in Zeile 2 und 3 das <mark>pick</mark> mit <mark>squash</mark>. Das "pick" in der ersten Zeile wird nicht geändert. Abschließend speichert man das ganze ab. 

Nun sollte erneut ein Editor geöffnet werden in dem man bei Bedarf die Commit-Nachricht anpassen kann. Da ich für alle drei Commits die gleiche Nachricht genutzt hatte, habe ich keine Änderungen vorgenommen.

Abschließend führt man noch <mark>git push --force origin HEAD</mark> aus um die Änderungen an Github zu senden. Sollte man einen anderen Alias für das Repository genutzt haben (origin ist Standard) muss man den Befehl entsprechend anpassen. Wer sich nicht sicher ist, kann in der Datei config im Verzeichnis .git nachsehen das im lokalen Arbeitsverzeichnis zu finden ist.

Sofern man nicht die einzige Person ist, die an den Dateien Änderungen vornimmt, sollte man anstelle --force besser [--force-with-lease](https://git-scm.com/docs/git-push#Documentation/git-push.txt---no-force-with-lease) nutzen.

Schaut man sich nun die Historie des Repository an, wurden die betreffenden Commits zu einem Commit zusammengefasst.
