---
title: Fenstertitel von Terminator in Verbindung mit der ZSH
date: 2014-07-20T22:17:00+0100
categories:
- Linux
- OSBN
tags:
- Terminator
- ZSH
- Fenstertitel
- Shell
slug: fenstertitel-von-terminator-in-verbindung-mit-der-zsh
---
Als Terminal-Emulator setze ich, wie in [einem anderen Artikel](https://fryboyter.de/ich-muss-terminieren "Terminator Terminal Emulator") bereits geschrieben, Terminator ein. In Verbindung mit der ZSH gibt es hier allerding etwas, dass mich stört. Und zwar wird als Fenstertitel immer /bin/zsh angezeigt.

![Bin ZSH](/files/bin-zsh_001.png)

Um das zu ändern, muss man die Datei .zshrc anpassen, welche man im Home-Verzeichnis findet. In dieser fügt man folgendes ein.

<pre><code class=\"language-bash\">case $TERM in xterm*) precmd () {print -Pn \"\\e]0;%~\\a\"} ;; esac</code></pre>

Speichert man die Date nun und öffnet eine neue Instanz von Terminator, erhält man folgenden Titel angezeigt.

![Titel ZSH](/files/titel_zsh_2.png)

Was als Titel angezeigt wird, definiert man mittels print -Pn "\e]0;%~\a". In diesem Beispiel wird einfach das Verzeichnis angezeigt, in dem man sich gerade befindet. Das Home-Verzeichnis wird hierbei mit dem üblichen ~ abgekürzt. Nimmt man stattdessen print -Pn "\e]0;%n@%m: %~\a" erhält man den Titel Benutzername@Hostname: Aktuelles Verzeichnis. Die ganzen Prompt Escapes wie %~ oder %n usw. kann man [hier](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html "Prompt Escapes") nachlesen. Somit lässt sich die Anzeige an die eigenen Wünsche anzeigen.
