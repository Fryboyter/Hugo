---
title: Wörterliste für Diceware erstellen
date: 2018-02-02T15:57:20+0100
categories:
- Linux
- OSBN
tags:
- Diceware
- Wörterliste
slug: woerterliste-fuer-diceware-erstellen
---
Bei Diceware handelt es sich um ein Verfahren mit dem man lange, aber leichter zu merkende Passwörter erstellen kann. Hierzu braucht man einen Würfel und eine Liste mit Wörtern.

In dieser Liste findet man pro Zeile ein Wort dem eine fünfstellige, einzigartige Zahl vorangestellt ist. Will man nun zum Beispiel ein Passwort aus 5 Wörtern erstellen, muss man pro Wort 5 mal würfeln. Also insgesamt 25 mal. Am Ende hat man dann beispielsweise 54678 29412 37783 79381 erwürfelt. Nun schnappt man sich besagte Liste und sucht die betreffenden Wörter. Somit könnte beispielsweise DachsPlastikrodelnEinkaufFluss herauskommen. Wichtig hierbei ist, dass man die Wörter nicht neu würfelt oder sich eigene Wörter ausdenkt, wenn man mit dem Ergebnis nicht zufrieden ist.

Im Internet gibt es diverse Wörterlisten für Diceware. Zum Beispiel unter [http://world.std.com/~reinhold/diceware.html](http://world.std.com/~reinhold/diceware.html). Diese ist aber inzwischen so bekannt, dass sie vermutlich schon von Crackern benutzt wird und zum anderen sind dort "nur" knapp 7800 Wörter enthalten.

Nehmen wir nun an, man trifft im Internet die Aussage, dass man Diceware nutzt. Somit steht die Chance für die bösen Buben nicht schlecht, dass man die offizielle Liste mit den Wörtern nutzt. Dies macht die Aufgabe das Passwort zu knacken schon etwas einfacher. Daher wäre eine eigene Liste wohl nicht verkehrt. Dies kann man mit folgendem Script erledigen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">wget "https://www.openthesaurus.de/export/OpenThesaurus-Textversion.zip"
wait
unzip OpenThesaurus-Textversion.zip
wait
grep -v '^#' openthesaurus.txt | \
tr ';' '\n' | \
tr [ÄÖÜ] [äöü] | \
grep  -v '[^[:alnum:] _]' | \
grep -v '[0-9]' | \
grep -v ' ' | \
grep -E '^.{3,8}$' | \
sort -uR | \
head -n 10000 | \
sort | \
nl -n rz -v 0 -w 4 > 'wordlist_de.txt'</code>
</pre>


Das Script macht zusammengefasst folgendes:

* Herunterladen und Entpacken der OpenThesaurus-Textversion (deutlich mehr als 7800 Worte)
* Je einen Eintrag in jeweils eine Zeile packen
* Filtern der Einträge mit Umlaute, Unterstrich oder Zahlen sowie Einträge die aus mehreren Wörtern bestehen
* Entfernen aller Wörter mit weniger als 3 und mehr als 8 Zeichen
* Entfernen eventueller doppelter Einträge
* Zufällige Sortierung der restlichen Einträge<
* Übernahme der ersten 10000 Einträge
* Alphabetische Sortierung dieser Einträge
* Nummerrierung der Einträge und das Abspeichern in die Datei "wordlist_de.txt"

Anhand dieser Liste lässt sich nun mittels eines Würfels ein Passwort aus einem großeren Pool an Wörtern erstellen. Wer hierzu keine Lust hat, kann auch Tools [diceware](https://github.com/ulif/diceware) nutzen. Diese kommen mit oben erstellter Liste auch zurecht. Es ist allerdings zu empfehlen wirklich selbst zu würfeln. Was die Anzahl der Wörter betrifft, sollte man aktuell mindestens 6 Wörter würfeln. Mehr sind natürlich besser. Wer will kann zwischen die Wörter noch ein Sonderzeichen oder ein Leerzeichen einfügen. Das erhöht die Sicherheit noch einmal.
