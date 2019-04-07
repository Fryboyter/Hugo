---
title: ZSH-Alias mit Platzhalter
date: 2018-05-22T17:54:00+0100
categories:
- Linux
- OSBN
tags:
- ZSH
- Alias
- Platzhalter
slug: zsh-alias-mit-platzhalter
---
Derzeit teste ich mal wieder AUR-Helper. Da ich mir die Paramenter usw. nicht merken will, lege ich ich normalerweise Aliase an. Für das Suchen im AUR wäre ein möglicher Alias zum Beispiel alias aurs='trizen -Ssa'. Derzeit teste ich den AUR-Helper aurman.

Hier wäre der Befehl nur im AUR nach Paketen zu suchen aurman -Ss Suchbegriff --aur. Da in diesem Fall der Suchbegriff mitten im Befehl steht klappt ein Alias wie aurs='aurman -Ss --aur' nicht wirklich. In den Alias einen Platzhalter zu packen (aurs='aurman -Ss $1 --aur') funktioniert ebenfalls nicht. Die Lösung hierfür ist kein Alias sondern eine Funktion.

Hierfür legen wir uns am besten ein extra Verzeichnis im Home-Verzeichnis an. Beispielswese .zfunc. In diesem erstellen wir nun die Datei aursearch und füllen diese mit folgendem Inhalt und speichern diese anschließend.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">function aurs() {
aurman -Ss $1 --aur
}</code>
</pre>

Anstelle von aurs geben wir den Namen ein über den wir die Funktion aufrufen wollen. Da bei mir die Aliase für den AUR-Helper normalerweise aurs (suchen), auri (installiere) und auru (aktualisieren) lauten habe ich mich hier für aurs entschieden.

Damit die Funktion automatisch zur Verfügung steht öffnen wir nun noch die Konfigurationsdatei von zsh (normalerweise .zshrc) und fügen dort folgende Zeile ein.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">source ~/.zfunc/aursearch</code></pre>

Hierbei ist zu beachten dass man den Namen der Datei angibt und nicht den Befehl mit dem man die Funktion ausführt.

Von nun an kann man nun mittels aurs Suchbegriff im AUR nach Paketen suchen. Eventuell vorhanden Aliase mit dem gleichen Namen sollte man aber vorher löschen bzw. auskommentieren.
