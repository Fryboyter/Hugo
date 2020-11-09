---
title: Bestimmte Zeile aus einer Datei entfernen
date: 2015-09-21T11:28:00+0100
categories:
- Linux
- OSBN
tags:
- Datei
- Teile
- Entfernen
slug: bestimmte-zeile-aus-einer-datei-entfernen
---
Gestern habe ich wieder mit mehreren Terminals unter terminator geöffnet. Weil es natürlich schnell gehen sollte, habe ich ein Passwort in den falschen Terminal eingegeben, so dass das Passwort quasi als Befehl in der History-Datei von zsh gelandet ist. Mal wieder. Nicht gerade das Gelbe vom Ei. Da mir leider keine Funktion unter der zsh bekannt ist, mit der man einzelne Zeilen aus der History-Datei entfernen kann, ist wieder Handarbeit angesagt gewesen. Je nach Lust und Laune nehme ich entweder einen Editor meiner Wahl (in der Regel nano oder kate), öffne die Datei ~/.zhistory und entferne den problematischen Eintrag. Oder ich verwende

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">grep -v $suchbegriff .zhistory &gt; tempdatei &amp;&amp; mv tempdatei .zhistory</code>
</pre>

Hierbei suche ich nach dem gewünschten Suchbegriff und leite alles was nicht diesem entspricht in die Datei tempdatei um (-v bewirkt dies). Danach überschreibe ist die Datei .zhistory mit der tempdatei, so dass ich eine bereinigte History-Datei erhalte. Da bekanntlich unter Linux viele Wege zum Ziel führen, habe ich gestern eine etwas weniger umständliche Alternative mittels sed gefunden.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">sed -i '/suchbegriff/d' .zhistory</code>
</pre>

Der Parameter -i weist sed an, die Änderungen direkt in der .zhistory vorzunehmen und auch direkt zu speichern. Sollen solche "Aufräum-Befehle" ebenfalls nicht in der History-Datei landen, sollte man bevor man anfängt sicherstellen, dass in der Datei ~/.zshrc der Eintrag

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">setopt HIST_IGNORE_SPACE </code>
</pre>

vorhanden ist. Fügt man nun vor dem eigentlichen Befehl ein Leerzeichen ein, so erscheinen diese nicht in der History-Datei. Dies gilt ebenfalls mit Aliase.
