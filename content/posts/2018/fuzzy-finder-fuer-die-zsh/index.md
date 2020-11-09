---
title: Fuzzy Finder für die ZSH
date: 2018-08-20T21:42:00+0100
categories:
- Linux
- OSBN
tags:
- ZSH
- Fuzzy Finder
slug: fuzzy-finder-fuer-die-zsh
---
Gestern hatte ich in einem Anfall von Wahnsinn meine Konfiguration der ZSH\_aufgeräumt. Anstelle von zwei Dateien habe ich nun sieben mit ziemlich viel Kommentaren. Dafür kann man endlich nachvollziehen welcher Eintrag was macht und es ist alles ordentlicher. Nur beim Aufräumen ist aber nicht geblieben.

Die Suchfunktion in der Historie hat mir in letzter Zeit irgendwie nicht mehr zugesagt. Daher habe ich [fzf](https://github.com/junegunn/fzf) (command-line fuzzy finder) getestet. Nach dem Installieren das Pakets muss man nur folgende Einträge in die .zshrc eintragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">source /usr/share/fzf/key-bindings.zsh
source /usr/share/fzf/completion.zsh</code>
</pre>

Wenn man nun mittels Strg + R in der Historie suchen will erhält man erst einmal eine etwas ungewohnte Anzeige, die aus den letzten Einträgen besteht. Erst einmal nichts besonderes. Sucht man aber beispielsweise nach "pac" für pacman, bekommt man schon deutlich besser aufbereitet Ergebnisse angezeigt.

{{< image src="fzf1.png" alt="fzf zsh" >}}

Mit den Cursor-Tasten lässt sich dann der gewünschte Eintrag auswählen. Angezeigt werden wohl standardmäßig immer 8 Einträge. Wenn mehr Einträge vorhanden sind, kann man allerdings auch weiter nach oben scrollen.

Fzf lässt sich aber nicht nur für die Historie der Shell nutzen. Verwendet man anstelle von Strg + R Strg + T kann man "fuzzy" nach Dateien und Verzeichnissen suchen. Hierbei wird allerdings das normale find verwendet. Somit ist zumindest dieser Teil, gerade bei vielen Dateien nicht gerade schnell. So wie der Sourcecode aussieht kann man diesen aber vermutlich schnell anpassen, dass statt dessen das schnellere fd verwendet wird. Ein weiterer Shortcut wäre ALT + S mit dem man nach Verzeichnissen suchen und direkt in diese wechseln kann.

Alles in allem konnte ich mit fzf nun drei Erweiterungen komplett ablösen. Diese habe zwar keine Probleme gemacht, aber weniger ist ab und zu auch mehr. Fzf sollte meines Wissens nach auch unter Fish und Bash funktionieren.
