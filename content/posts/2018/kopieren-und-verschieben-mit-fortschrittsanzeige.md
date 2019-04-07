---
title: Kopieren und Verschieben mit Fortschrittsanzeige
date: 2018-02-15T20:18:00+0100
categories:
- Linux
- OSBN
tags:
- Fortschrittsanzeige
- Kopieren
- Verschieben
slug: kopieren-und-verschieben-mit-fortschrittsanzeige
---
Heute morgen hatte ich eine Datei mit 35 Gigabyte kopiert. Nach ein paar Minuten war ich mir unsicher ob der Vorgang noch läuft oder eventuell hängen geblieben ist. Hier wäre mir eine Fortschritsanzeige recht lieb gewesen.

Der Befehl cp bietet diese Funktion leider nicht an, und da er als "feature complete" gilt wird er es auch nie. Nach etwas Google Fu habe ich neben rsync das Projekt pycp gefunden. In diesem sind die Befehle pycp und pymv enthalten. Erster ist ein Ersatz für cp und zweiter für mv. Und alle beide bieten eine Anzeige für den Fortschritt, die Datenübertragungsrate und die geschätzte verbleibende Zeit. Das ganze sieht dann beispielsweise wie folgt aus. Anstelle von pycp kann man auch pymv nutzen um Dateien zu verschieben.

<img alt="pycp Screenshot" src="/files/pycp.png" style="width: 656px; height: 201px;">

Natürlich kann man das auch mit Konstrukten wie cp "file" "destination" &amp;&amp; pv $(pidof cp) oder rsync -avP &lt;Quelle&gt; &lt;Ziel&gt; arbeiten. Aber pycp große_datei ~/Downloads ist mir einfach lieber. Hier siegt die Faulheit und ich installiere mir lieber ein Tool mehr auf den Rechner.
