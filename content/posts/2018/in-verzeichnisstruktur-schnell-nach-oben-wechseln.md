---
title: In Verzeichnisstruktur schnell nach oben wechseln
date: 2018-09-19T19:19:00+0100
categories:
- Linux
- OSBN
tags:
- Verzeichnisstruktur
- Wechseln
slug: in-verzeichnisstruktur-schnell-nach-oben-wechseln
---
Ab und zu muss ich in einer Verzeichnisstruktur arbeiten die ziemlich verästelt ist. Wenn man in dieser dann zum Beispiel zwei Ebenen nach oben will, kann man cd ../.. nutzen. Will man aber zum Beispiel sechs Ebenen höher, muss man schon aufpassen, dass man ensprechend viele .. und / eingibt.

Um dies zu vereinfachen, kann folgende Funktion genutzt werden (getestet mit der zsh).

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">function up {
     
    local counter=${1:-1}
    local dirup="../"
    local out=""

    while (( counter > 0 )); do
        let counter--
        out="${out}$dirup"
    done

    cd $out
}</code>
</pre>

Befindet man sich beispiel in /etc/systemd/system/timer.target.wants und will in /etc/systemd/systemd\_wechseln, reicht mit dieser Funktion der Befehl "up 2" aus.
