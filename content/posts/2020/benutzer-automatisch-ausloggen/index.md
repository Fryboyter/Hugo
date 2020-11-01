---
title: Benutzer automatisch ausloggen
date: 2020-06-08T00:40:55+0200
categories:
- OSBN
- Linux
tags:
- Benutzer  
- Root
- Ausloggen
slug: benutzer-automatisch-ausloggen
---
Ich gehöre zu den Leuten die sudo nur für bestimmte Befehle und nicht als Ersatz von root nutzen. In fast allen Fällen bin ich so konsequent und beende die Sitzung mit Root-Rechten im Terminal Emulator nachdem ich diese Rechte nicht mehr benötige. Aber eben nur fast immer.

An sich ist das kein Problem, da ich alleiniger Nutzer meiner Rechner bin. Aber sicher ist sicher. Als Lösung kann man die Variable TMOUT nutzen. Mit dieser kann man definieren nach wie vielen Sekunden Inaktivität die jeweilige Session beendet wird. Inaktivität bedeutet hierbei, dass keine Eingabe über die Tastatur erfolgt.

Hierzu legt man die Datei /etc/profile.d/bash_autologout.sh an und trägt in diese folgendes ein.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">TMOUT=600
readonly TMOUT
export TMOUT</code>
</pre>

Bei diesem Beispiel wird nach 600 Sekunden, also 10 Minuten, die jeweilige Session beendet. Dies betrifft sowohl Benutzerkonten als auch root. Diesen Wert kann man nach Belieben anpassen. Mit "readonly TMOUNT" verhindert man, das man die Veriable im laufenden Betrieb ändern kann (z. B. mit unset TMOUT). Wer diese Möglichkeit weiterhin haben will, trägt die Zeile einfach nicht ein. Führt man einen Befehl aus der länger als der angegebenen Zeitraum läuft (z. B. sleep 650 && echo "Hallo Welt"), beginnt der Countdown erst nachdem der Befehl fertig ist. Wer nicht will, das auch normale Benutzer im Terminal Emulator ausgeloggt werden, verzichtet einfach darauf die Zeile "export TMOUT" einzutragen.
