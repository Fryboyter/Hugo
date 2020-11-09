---
title: WLAN Stick und Predictable Network Interface Names
date: 2018-12-19T23:28:00+0100
categories:
- Linux
- OSBN
tags:
- Fritz
- WLAN
- AC 860
- Udev
slug: wlan-stick-und-predictable-network-interface-names
---
[Predictable Network Interface Names](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) sind im Grunde eine gute Sache, da der zugeteilte Name des Interfaces immer gleich bleibt. Bei einem USB-WLAN-Stick kann es aber auch nerven.

Wie heute schon geschrieben, habe ich mir den Fritz!WLAN Stick AC 860 zugelegt. Diesen habe ich bei ersten Tests in den USB-Port auf der rechten Seite des Notebooks gesteckt. Der Befehl "ip addr" hat dann zum Beispiel "wlp0s26u1u2" als Interface-Name ausgspuckt, welchen ich in die Konfigurationsdatei von netctl eingetragen habe. Nachdem alles funktioniert hat, habe ich noch etwas herumgespielt und hierbei den Stick auch in den USB-Port auf der linken Seite gesteckt. Und schon konnte ich die Netzwerkverbindung nicht aufbauen. Ein erneutes Ausführen von "ip addr" hat mir nun den Interface-Namen "wlp0s20u2" angezeigt.

Im Grunde genommen ist das auch logisch, da es sich um einen anderen Steckplatz handelt und daher auch ein anderer Name fest zugeteilt wird. Aber in der Praxis ist das ungünstig, da in der Konfiguration von netctl der Interface-Name fix eingetragen wird. Muss ich also zukünftig darauf achten, den Stick immer in den gleichen Port zu stecken? Entweder das oder man erstellt sich eine udev-Regel.

Hierzu schließt man erst einmal den Stick an und führt danach "lsusb" aus. Hiermit erhält man beispielsweise folgende Ausgabe.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">Bus 001 Device 004: ID 057c:8503 AVM GmbH</code>
</pre>

Nun prüft man, wie udev den Stick sieht. Hierzu führt man folgenden Befehl aus.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">udevadm info -a -p $(udevadm info -q path -n \_/dev/bus/usb/001/004) | grep ATTR{configuration} </code>
</pre>

Hier muss man den Teil mit /dev/bus/usb entsprechend der Ausgabe von lsub anpassen. Im Falle des von mir verwendeten Sticks wird "ATTR{configuration}=="FRITZ!WLAN AC 860"" ausgegeben.

Nun hat man alles, was man für eine udev-Regel braucht. Unter /etc/udev/rules.d/ erstellt man daher die Datei 10-network-devices.rules mit folgendem Inhalt und speichert diese ab. Nutzt man einen anderen Stick, muss man logischerweise bei ATTRS{product} etwas anderes eintragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">SUBSYSTEM=="net", ACTION=="add", ATTRS{product}=="FRITZ!WLAN AC 860", NAME="wlan"</code>
</pre>

Schließt man zukünftig einen Netzwerkadapter über USB an, wird geprüft ob dieser das Produkt-Attribut "FRITZ!WLAN AC 860" hat. Wenn ja, wird diesem der Interface-Name "wlan" zugeteilt. Und zwar egal an welchem USB-Anschluss der Stick angeschlossen wurde.

Vielleicht ist es dem einen oder anderen aufgefallen, dass bei dem Befehl mit udevadm ATTR{product} angezeigt wird, in der Regel aber ATTRS{product} steht. Das ist kein Fehler, sondern muss in diesem Fall so sein.
