---
title: Teile des Pfads bis zum Slash unter der ZSH löschen
date: 2018-01-27T15:05:00+0100
categories:
- Linux
- OSBN
tags:
- ZSH
slug: teile-des-pfads-bis-zum-slash-unter-der-zsh-loeschen
---
Nehmen wir einmal an, dass in der Historie der ZSH der Befehl "cd /home/nutzer/Downloads/Filme/Action" vorhanden ist. Was aber, wenn man nur in den Ordner Downloads wechseln will?

Eine Möglichkeit wäre, den Befehl aus der Historie aufzurufen und einfach Filme/Action zu löschen bevor man den Befehl ausführt. Oder man drückt einfach ALT + Backspace. Hier macht die ZSH allerdings Probleme. Anstelle bis beispielsweise rückwärts bis zum nächsten Slash zu löschen, wird bis zum nächsten Leerzeichen gelöscht. Somit wird aus "cd /home/nutzer/Downloads/Filme/Action" mit nur einem Shortcut "cd". Irgendwie blöd. Also muss mal wieder meine .zshrc erweitert werden. In diese habe ich folgende Funktion gepackt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">function backward-kill-partial-word {
         local WORDCHARS="${WORDCHARS//[\/.]/}"
         zle backward-kill-word "$@"
     }
     zle -N backward-kill-partial-word
     for x in '^Xw' '^[^?' '^[^H'; do
         bindkey "$x" backward-kill-partial-word
     done; unset x</code>
 </pre>

 Mittels WORDCHARS wir hierbei definiert, dass auch / Teil eines Worts ist. Speichert man nun die .zshrc und läd diese mittels "source ~/.zshrc" erneut ein lässt sich nun ein eingegbener Pfad mittels ALT + Backspace bis zum jeweils nächsten Slash rückwärts löschen.
