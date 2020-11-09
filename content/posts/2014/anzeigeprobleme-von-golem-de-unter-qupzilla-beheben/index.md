---
title: Anzeigeprobleme von golem.de unter QupZilla beheben
date: 2014-05-26T09:13:00+0100
categories:
- OSBN
- Allgemein
tags:
- QupZilla 
- Anzeigeprobleme
- Golem
slug: anzeigeprobleme-von-golem-de-unter-qupzilla-beheben
---
Wer hier regelmäßig liest, hat bestimmt schon mitbekommen, dass ich aktuell den Browser QupZilla nutze. Dieser hat allerdings mit golem.de ein Problem. Ab einer gewissen Länge der Artikelüberschriften werden diese auf zwei Zeilen umgebrochen. Leider hat dies zur Folge dass sich die zweite Zeile mit dem Artikeltext überlappt. Was ziemlich unschön aussieht.

{{< image src="qupzilla_golem.png" alt="qupzilla_golem" >}}

Das Problem habe ich schon dem Entwickler gemeldet, aber bis es eine Reaktion oder Lösung gibt, muss erst mal ein Workaround her. Unter Opera hätte ich einfach eine, nur für golem.de gültige, CSS-Datei erstellt. Leider bietet [QupZilla](http://www.qupzilla.com "QupZilla") das aktuell nicht an. Nur eine globale CSS-Datei wäre möglich. Das ist mir zu unsicher. Also sind größere Geschütze nötig. Unter QupZilla gibt es das Plugin [Greasemonkey](http://de.wikipedia.org/wiki/Greasemonkey "Greasemonkey"). Für solche Kleinigkeiten ist es eigentlich nicht gedacht, aber was soll's. Erst einmal muss das Plugin in den Einstellungen aktiviert werden.

{{< image src="qupzilla_golem2.png" alt="qupzilla_golem2" >}}

Wenn das Plugin aktiviert ist, klickt man am besten auf die Schaltfläche "Einstellungen" und dort dann auf "Script-Verzeichnis öffnen". In dem nun angezeigten Verzeichnis werden die Greasemonkey-Scripte abgelegt. Von daher erstellen wir dort die Datei golem.user.js. Anstelle von golem kann man nehmen, was man will. An user.js darf man allerdings nichts ändern, da es sonst nicht funktioniert. Die erstellte Datei öffnen wir nun mit einem Editor nach Wahl und tragen dort folgendes ein.

<pre>
<code class="language-bash">// ==UserScript==
// @name          Golem Uberschrift 
// @include       http://www.golem.de/* 
// @run-at        document-start 
// ==/UserScript==
GM_addStyle(".head1 {position: static !important; top: -2px; }");
</code>
</pre>

Bei @name kann man eintragen, was man will. Dies wird dann im Browser angezeigt. Bei @include wird hinterlegt, für welche Seite(n) das ganze gültig ist. Und @run-at definiert, wann das ganze ausgeführt werden soll. Mittels GM_addStyle fügt CSS-Anweisungen in den Quelltext der betreffenden Seite ein und überschreibt somit quasi die ursprünglichen Angaben. Mittels des Web Inspectors des Browsers habe ich mich durch die Seite geklickt und .head1 als das "Problem" indentifiziert. Von daher habe ich es mittels [GM_addstyle](http://wiki.greasespot.net/GM_addStyle "GM_addstyle") von .head1 {position: absolute; top: -2px; } auf .head1 {position: static !important; top: -2px; } umgebogen. Vermutlich nicht ganz die feine englische Art, aber es funktioniert und macht in dem Fall keine weiteren Probleme.

Die Datei speichert man dann einfach ab und startet den Browser einmal neu. Ruft man nun die Einstellungen des Plugins auf, sollte man folgende Anzeige erhalten.

{{< image src="qupzilla_golem3.png" alt="qupzilla_golem3" >}}

Eventuell, falls es nicht schon der Fall ist, muss man hier noch den Haken setzen um das ganze zu aktivieren. Danach sollte die Anzeige der Überschriften bei golem.de unter QupZilla wieder passen.

{{< image src="qupzilla_golem4.png" alt="qupzilla_golem4" >}}
