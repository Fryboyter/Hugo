---
title: Mausgesten unter Vivaldi händisch anpassen
date: 2015-09-11T14:43:00+0100
categories:
- Linux
- OSBN
tags:
- Vivaldi
- Browser
- Mausgesten
slug: mausgesten-unter-vivaldi-haendisch-anpassen
---
Offiziell kann man die Mausgesten unter dem Browser Vivaldi noch nicht anpassen oder gar neue hinzufügen. Zumindest das Anpassen klappt aber indem man eine Datei händisch ändert.

Ausgehend vom aktuellen Snapshot findet man unter /opt/vivaldi-snapshot/resources/vivaldi/ die Datei defaultSettings-bundle.js. Diese öffnet man mit einem Editor seiner Wahl. In dieser findet man Einträge wie z. B.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">COMMAND_CLOSE_TAB:{shortcut:["ctrl+w",\"ctrl+f4"],gestures:["20"]</code>
</pre>

Wichtig ist hier der Teil gestures:["2"]. Die Zahl(en) definieren hier die Mausgesten. 2 entspricht nach unten, 4 nach links, 0 nach rechts und 6 nach oben. Tauscht man nun die bestehende Nummer gegen die gewünschte aus, kann man die Mausgesten nach seinem Geschmack anpassen. Die Nummern kann man auch miteinander kombinieren. In obigen Beispiel für das Schließen eines Tabs ist also nach unten und dann nach rechts definiert.

Bei diesem Vorgehen sollte man allerdings beachten, dass die Datei voraussichtlich beim nächsten Update wieder überschrieben wird und man die Datei somit erneut anpassen muss. Wem das zu Umständlich ist, sollte abwarten bis die Mausgesten offiziell anpassbar sind. Dies ist nach meiner Kenntnis seitens der Entwickler auch geplant.

Gefunden hat diese Lösung übrigens der Nutzer shoust vom Vivaldi-Forum. Ich habe das ganze nur etwas ausführlicher und in deutscher Sprache wiedergegeben.
