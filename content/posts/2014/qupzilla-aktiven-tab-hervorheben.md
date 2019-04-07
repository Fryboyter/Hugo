---
title: QupZilla - aktiven Tab hervorheben
date: 2014-03-28T11:42:00+0100
categories:
- OSBN
- Allgemein
tags:
- Qupzilla
- Tab
slug: qupzilla-aktiven-tab-hervorheben
---
Wie inzwischen hinlänglich bekannt sein sollte, suche ich einen für mich adäquaten Ersatz für Opera 12.16. So wie es aussieht, werde ich nun wohl erst einmal bei QupZilla landen, über den ich hier schon einmal einen [Artikel](https://fryboyter.de/qupzilla-noch-eine-alternative-zu-opera-12-16 "Qupzilla") geschrieben habe. Die vorhandenen Mausgesten sind im Auslieferungszustand zwar weiterhin nur über die mittlere Maustaste steuerbar, aber laut [diesem](https://github.com/QupZilla/qupzilla/issues/386 "Mausgesten anpassen Qupzilla") Ticket ist wohl jemand bereits an der Sache dran, um dies zu ändern. Bis dahin werde ich mir wohl eigene Mausgesten mit easystroke [basteln](https://fryboyter.de/mausgesten-der-marke-eigenbau). Für Windows muss ich mich noch für ein vergleichbares Programm entscheiden.

Was mich bisher unter QupZilla aber noch recht stört ist die Tatsache, dass bei jedem mitgeliefertem Theme der derzeit aktuelle Tab einfach nur weiß ist. Das sieht bei einer Seite die den gleiche Hintergrundfarbe nutzt, nicht gerade gut aus.

<a href="/files/QupZilla4.png"><img alt="QupZilla1" src="/files/QupZilla4.png" style="width: 300px; height: 70px;"></a>

Da der Browser viel mit CSS macht, habe ich mir mal die Datei main.css angesehen. Dort wird leider nichts definiert, was mit dem aktiven Tab zu tun hat. Wäre ja auch zu einfach gewesen. Nachdem ich Google mal wieder etwas gequält habe, bin ich darauf gestoßen, dass es unter Qt die Klasse QTabBar gibt und den "Zustand" tab:selected. Keine Ahnung wie man den Zustand korrekt nennt. Ist an der Stelle eigentlich auch egal. Nach ein paar Versuchen habe ich mir dann folgendes in der main.css zusammengebaut.

<pre>
<code class="language-bash">QTabBar::tab:selected {
background-color: #008000;
border-bottom-style: none;
</code>
</pre>

Und siehe da, es funktioniert und der aktive Tab erstrahlt nun in einem satten Grün.

<a href="/files/QupZilla5.png"><img alt="QupZilla2" src="/files/QupZilla5.png" style="width: 300px; height: 70px;"></a>

Das Ganze ist jetzt zwar noch verbesserungsfähig, aber immerhin ein Anfang. Wer sich an der ursprünglichen Farbe des aktiven Tabs gestört hat, hat nun einen Punkt an der er/sie ansetzen kann.

Somit bleibt aktuell nur noch ein Kritikpunkt übrig. Man kann die Icons für Vor, Zürück, Reload und Home nicht nach rechts verschieben. Wenn das noch kommt, bin ich happy.