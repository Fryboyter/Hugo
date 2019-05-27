---
title: Ripgrep - grep auf Steroide
date: 2017-01-12T18:59:00+0100
categories:
- Linux
- OSBN
tags:
- Ripgrep
- Grep
- Alternative
slug: ripgrep-grep-auf-steroide
---
Grep ist wohl das Standardtool um den Inhalt von Dateien zu durchsuchen. Allerdings braucht man oft sehr viele Geduld. Für Ungeduldige gibt es ripgrep.

Ripgrep ist eine Alternative zu grep, welche in Rust geschrieben ist und die in vielen Fällen deutlich schneller zu einem Ergebnis kommt als grep. Bei ersten Tests konnte ich deutliche Unterschiede feststellen. Ich habe spaßeshalber einmal das ganze Homeverzeichnis meines Notebooks durchsucht.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">grep -Ir Rybka /home/XYZ
/home/XYZ/Downloads/bundle.ini:[Rybka 2.2 32 bit]
/home/XYZ/Downloads/bundle.ini:ExeName=Rybka v2.2n2.mp.w32.exe
/home/XYZ/Downloads/bundle.ini:RelPath=\Engines\Rybka
/home/XYZ/Downloads/bundle.ini:[Rybka 2.2 64 bit]
/home/XYZ/Downloads/bundle.ini:ExeName=Rybka v2.2n2.mp.x64.exe
/home/XYZ/Downloads/bundle.ini:RelPath=\Engines\Rybka
/home/XYZ/Downloads/engines.ini:Rybka=Vasik Rajlich;USA
grep -Ir Rybka /home/XYZ 0,61s user 4,36s system 18% cpu 27,098 total</code></pre>

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">time rg -uu Rybka /home/XYZ
/home/XYZ/bundle.ini
23:[Rybka 2.2 32 bit]
24:ExeName=Rybka v2.2n2.mp.w32.exe
26:RelPath=\Engines\Rybka
32:[Rybka 2.2 64 bit]
33:ExeName=Rybka v2.2n2.mp.x64.exe
35:RelPath=\Engines\Rybka

/home/XYZ/Downloads/engines.ini
2666:Rybka=Vasik Rajlich;USA
rg -uu Rybka /home/XYZ 0,44s user 0,52s system 375% cpu 0,256 total</code></pre>

Wie man sieht, ist ripgrep hier leicht schneller. Andrew Gallant, der Entwickler von ripgrep, hat auf seinem Blog einen ausführlichen Artikel [veröffentlicht](http://blog.burntsushi.net/ripgrep), in dem neben diversen anderen Benchmarks genauer auf ripgrep eingegangen wird. Unter anderem auch für wen ripgrep eher nicht geeignet ist.
