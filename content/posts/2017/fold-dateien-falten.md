---
title: Fold - Dateien falten
date: 2017-11-06T18:59:31+0100
categories:
- Linux
- OSBN
tags:
- Fold
- Dateien falten
slug: fold-dateien-falten
---
Auch wenn man mehrere Jahre Linux nutzt, lernt man immer noch dazu. So ist mir heute der Befehl fold untergekommen, den ich bewusst wohl noch nie benutzt habe.

Nehmen wir mal die Ausgabe von "uname -a" als Beispiel. Diese sieht bei mir gerade inkl. Umbruch wie folgt aus.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">Linux notebook 4.13.11-1-zen #1 ZEN SMP PREEMPT Thu Nov 2 18:46:37 UTC 2017 x86_
n64 GNU/Linux</code>
</pre>

Übergibt man diese Ausgabe an fold (z. B. uname -a | fold -sw 30) bekommt man folgendes angezeigt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">Linux notebook 4.13.11-1-zen 
#1 ZEN SMP PREEMPT Thu Nov 2 
18:46:37 UTC 2017 x86_64
GNU/Linux
</code></pre>

Das sieht doch schon schöner aus. Aber was wird hier genau gemacht? Der Parameter "w 30" gibt an, dass ein Umbruch nach 30 Zeichen erfolgen soll. Der Parameter "s" verhindert zudem dass zum Beispiel innerhalb eines Wortes umgebrochen wird. Ein Umbruch erfolgt also nur bei einem Leerzeichen.
