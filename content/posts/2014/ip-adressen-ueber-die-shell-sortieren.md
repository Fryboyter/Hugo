---
title: IP-Adressen über die Shell sortieren
date: 2014-06-12T00:00:00+0100
categories:
- Linux
- OSBN
tags:
- IP-Adressen
- Sortierung
slug: ip-adressen-ueber-die-shell-sortieren
---
Ich habe hier eine Textdatei in der pro Zeile eine IP-Nummer steht. Allerdings geht es wild durcheinander. Ziel ist es nun die ganzen Nummern zu sortieren. Mittels folgendem Konstrukt konnte ich die ZSH (sollte auch mit Bash und Co funktionieren) überreden die Nummern zu ordnen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">cat unsortiert.txt | sort -n -t . -k 1,1 -k 2,2 -k 3,3 -k 4,4 | uniq &gt;&gt; sortiert.txt
</code>
</pre>

Doppelt aufgeführte Nummern werden hierbei auch gleich auf einen Eintrag minimiert.
