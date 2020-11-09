---
title: Caddy Webserver
date: 2018-11-28T20:44:00+0100
categories:
- OSBN
- Allgemein
tags:
- Caddy
- Webserver
slug: caddy-webserver
---
Heutzutage sind die Webserver Apache und nginx weit verbreitet. Selbst nutzt ich nginx um damit eine Paketquelle für selbst erstellte Arch-Pakete im LAN anzubieten. Was die Konfiguration betrifft, kann nginx allerdings etwas umständlich sein.

Heute habe ich mir einmal den Webserver [Caddy](https://caddyserver.com) angesehen. Dieser ist mit Go erstellt und wird seit 2015 aktiv weiterentwickelt. Auf der Downloadseite kann man sich seine eigene Caddy-Datei erstellen in dem man die Plattform wie ARMv7 und eventuelle Plugins auswählt. Ist dies erledigt, wird auch ein Link angezeigt mit dem man sich die Datei mit den gewünschten Einstellungen automatisch herunterladen kann (z. B.https://caddyserver.com/download/linux/arm7?plugins=http.expires&amp;license=personal&amp;telemetry=off). Leider schlägt auch Caddy in die gleiche Kerbe wie Pi Hole und bietet eine alternative Installation in Form von beispielsweise curl https://getcaddy.com | bash -s http.expires an. Das geht eigentlich gar nicht.

Was mir an Caddy besonders gefällt, ist die Konfiguration. So könnte diese zum Beispiel wie folgt aussehen:

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">192.168.1.2:8888
root /verzeichnis/zum/Webroot
gzip
browse</code>
</pre>

Der Server ist also über die IP 192.168.1.2 auf Port 8888 erreichbar. Der Webroot ist /verzeichnis/zum/Webroot und gzip sowie Directory Listing sind aktiviert.

Ein Reverse Proxy lässt sich ebenfalls in Sekunden erstellen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">abc.com {
    proxy / localhost:8181
}</code>
</pre>

Nett finde ich auch die Tatsache, dass Let's Encrypt von Haus aus genutzt wird, ohne etwas machen zu müssen (lässt sich bei Bedarf aber deaktivieren bzw. genauer einstellen). Auf der [Seite](https://caddyserver.com) von Caddy findet man eine leicht Verständliche Dokumentation für den gesamten Server sowie diverse Konfigurationsbeispiele.

Der Sourcecode von Caddy wird unter der Apache Lizenz 2.0 veröffentlicht. Wer die fertigen Binär-Dateien nutzen will, kann dies für den privaten Einsatz kostenlos tun. Im Unternehmensbereich muss allerdings ein monatlicher Beitrag gezahlt werden. Ein Erstellen aus dem Sourcecode ist natürlich kostenlos möglich.