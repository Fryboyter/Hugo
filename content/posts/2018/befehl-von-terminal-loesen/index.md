---
title: Befehl von Terminal lösen
date: 2018-07-16T23:03:00+0100
categories:
- Linux
- OSBN
tags:
- Befehle
- Terminal
- Lösen
slug: befehl-von-terminal-loesen
---
Ich habe heute Abend etwas mit KeepassXC und KeepassXC-Browser herumgespielt und KeepassXC im Terminal Emulator gestartet. Nun wollte ich diesen beenden ohne das KeepassXC beendet wird.

Da ich KeepassXC ganz normal mit keepassxc gestartet habe, würde das Schließen des Terminal Emulators auch das Beenden von KeepassXC bedeuten. Aber dies lässt sich wie folgt verhindern.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">Strg + Z
bg
disown %1</code>
</pre>

Mit der ersten Zeile legen wir den Prozess schlafen. Mit der zweiten Zeile befördern wir den Prozess in den Hintergrund. Und mit der dritten Zeile lösen wir den Prozess vom Terminal Emulator ab. Nun kann man das Fenster des Terminal Emulators einfach schließen und der Prozess läuft unabhängig davon weiter.
