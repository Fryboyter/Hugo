---
title: Howdoi - Wie zum Geier ging das jetzt noch gleich?
date: 2015-03-23T21:32:00+0100
categories:
- Linux
- OSBN
tags:
- Shell
- Hilfe
- Howdoi
slug: howdoi-wie-zum-geier-ging-das-jetzt-noch-gleich
---
Wer nicht oft mit tar arbeitet, kennt das Problem vermutlich. Wie ging das Erstellen eines Archives jetzt noch gleich? Keine Ahnung... Also dann rufen wir eben mal man tar auf und ackern uns durch die Manpage. Alternativ dazu kann man jetzt das Tool [howdoi](http://blog.gleitzman.com/post/43330157197/howdoi-instant-coding-answers-via-the-command\ "howdoi") fragen. Will man also wissen, wie man ein tar-Archiv erstellt gibt man folgendes ein.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">howdoi create tar archive</code>
</pre>

Und howdoi antworte darauf mit

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">tar -cf backup.tar --exclude "www/subf3" www </code>
</pre>

Wirklich ausgereift ist das Tool aber scheinbar nicht. Auf die "Frage" **howdoi copy files** erhält man irgendwie nicht die richtige Ausgabe...

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">As toolkit mentions above, Apache Commons IO is the way to go, specifically FileUtils . copyFile() ;
it handles all the heavy lifting for you. And as a postscript, note that recent versions of
FileUtils (such as the 2.0.1 release) have added the use of NIO for copying files; NIO can
significantly increase file-copying performance , in a large part because the NIO routines
defer copying directly to the OS/filesystem rather than handle it by reading and writing
bytes through the Java layer. So if you're looking for performance, it might be worth checking
that you are using a recent version of FileUtils.</code></pre>
