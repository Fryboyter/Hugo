---
title: Bestimmte Zeilen aus der Historie entfernen
date: 2018-08-13T10:19:00+0100
categories:
- Linux
- OSBN
tags:
- Historie
- Zeilen entfernen
slug: bestimmte-zeilen-aus-der-historie-entfernen
---
Manche Sachen wie Passwörter oder andere sensible Daten sollten nicht in der Historie der Shell landen. Wenn ich daran denke, setze ich vor dem Befehl ein Leerzeichen, so dass der betreffende Befehl in der Historie erscheint. Oft denke ich aber nicht daran. Daher habe ich mir jetzt eine Funktion erstellt, mit der ich die Einträge schnell wieder entfernen kann.

Im Verzeichnis ~/.func liegen meine Funktionen. Dort habe ich einfach die Datei clrhist angelegt und mit folgendem Inhalt befüllt und abgespeichert.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">function clrhist() {
awk -i inplace -v rmv="$1" '!index($0,rmv)' "$HISTFILE"
}</code></pre>

Damit diese Funktion funktioniert, ist abschließend noch der Eintrag source ~/.zfunc/clrhist in der .zshrc nötig. Vermutlich sollte das ganze in dem Fall auch für andere Shells wie die bash funktionieren. Hier wäre der Eintrag dann in der .bashrc nötig.

Nehmen wir nun als Beispiel an, das wir in geistiger Umnachtung das Passwort "passwort123" als Befehl eingegeben haben. Mit clrhist passwort123 lässt sich der Eintrag nun aus der Historie der Shell tilgen. Hierbei werden aber auch Zeilen wie "echo passwort123" oder "grep passwort123 /etc" gelöscht.
