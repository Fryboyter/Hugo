---
title: Hooks unter Mercurial
date: 2019-05-05T10:31:55+0200
categories:
- OSBN
- Allgemein
tags:
- Mercurial
- Hooks
slug: hooks-unter-mercurial
---
Gestern hatte ich ja bereits einen [Artikel](/git-zu-mercurial-konvertieren/) veröffentlicht, der die Versionsverwaltung Mercurial betrifft. Das betreffende Projekt wurde bisher mit Git verwaltet. Hierbei gab es auch einige Hooks. Hiermit lassen sich zum Beispiel automatisch Befehle ausführen wenn ein neuer Commit hochgeladen wurde. Hierfür verwendet man den Hook "post-receive" wie ich es vor kurzem in einem [Beitrag](/fryboyter-wird-nun-mit-hugo-erzeugt/) beschrieben habe. Zu diesem hat Tux auch einen Kommentar abgegeben, dass dies zum Beispiel auch mit Mercurial möglich ist.

An sich absolut korrekt, aber entweder ist die Dokumentation verbesserungswürdig oder ich stand auf der Leitung. Ich gehe an der Stelle mal von letzterem aus.

Unter [https://www.mercurial-scm.org/wiki/Hook](https://www.mercurial-scm.org/wiki/Hook) wird das ganze beschrieben. Jedes mal wenn ich einen Commit einpflege, soll ein Hook ausgeführt werden. Also habe ich in der Konfigurationsdatei hgrc folgendes eintragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[hooks]
commit = /pfad/zur/Datei/commithook
</code>
</pre>

Unter /pfad/zur/Datei/ habe ich dann die Datei commithook angelegt und dort eben das Script eingetragen, dass ausgeführt werden soll. Anschließend habe ich die Datei ausführbar gemacht.

Es hat aber nicht funktioniert. Die Commits sind zwar angekommen, der Hook wurde aber nicht ausgeführt. Nach etwas Google-Fu habe ich dann auch gemerkt wieso. Der Commit-Hook funktioniert scheinbar nur, wenn man den Commit direkt im Repository macht. Nicht jedoch wenn man diesen per push einträgt.

Man muss daher in die Datei hgrc folgendes eintragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[hooks]
changegroup = /pfad/zur/Datei/commithook
</code>
</pre>

Damit wird der Hook dann auch immer bei einem Commit ausgeführt.
