---
title: Rechte von Dateien und Verzeichnissen als Oktalzahl anzeigen
date: 2015-10-27T01:15:00+0100
categories:
- Linux
- OSBN
tags:
- Rechte
- Verzeichnisse
- Dateien
- Oktalzahl
slug: rechte-von-dateien-und-verzeichnissen-als-oktalzahl-anzeigen
---
Heute wollte ich die Rechte eines Verzeichnis und der daran enthaltenen Dateien überprüfen, da scheinbar ein Script etwas Mist gebaut hat. Prinzipiell kann man sich die Rechte schnell und einfach mittels

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">ls -alR</code>
</pre>

anzeigen lassen. Allerdings werden hier die Rechte durch die bekannten Buchstabenkombinationen angezeigt (z. B. -rw-r--r--). Lieber wäre mir in diesem Fall aber die Ausgabe mit Oktalzahlen wie zum Beispiel 755. Der Befehl ls kann dies scheinbar nicht. Nach einigen Hin und Her konnte ich das Problem mittels

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">find .zsh -printf "%m %p\n"</code>
</pre>

lösen (anstelle von .zsh gibt man das Verzeichnis an, das überprüft werden soll). Die Ausgabe sieht wie folgt aus.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">700 .zsh
700 .zsh/cache
700 .zsh/cache/netbook
644 .zsh/cache/netbook/SYS_ALL_UNITS
644 .zsh/cache/netbook/SYS_REALLY_ALL_UNITS
755 .zsh/.zfunc
644 .zsh/.zfunc/extendedcd
644 .zsh/.zfunc/cd</code>
</pre>
