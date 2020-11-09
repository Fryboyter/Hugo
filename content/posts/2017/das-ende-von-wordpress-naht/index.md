---
title: Das Ende von Wordpress naht
date: 2017-04-01T16:37:00+0100
categories:
- OSBN
- Allgemein
tags:
- Wordpress
- Ende
- Bolt CMS
slug: das-ende-von-wordpress-naht
---
Vor einigen Monaten hatte ich hier schon mal geschrieben, dass ich Wordpress den Rücken kehren will. Als neue Plattform habe ich Bolt CMS gewählt. Der Wechsel ist in letzter Zeit aus beruflichen Gründen, aber auch weil ich wenig Lust hatte, ins Stocken geraten. Aber es geht in die nächste Runde.

Seit heute bin ich quasi in der Beta-Phase angekommen. Was das Template betrifft, habe ich es bewusst schlicht gehalten. Und das nicht nur weil ich von Grafikbearbeitung keine Ahnung habe.

{{< image src="fryboyter_beta.png" alt="Fryboyter Beta" >}}

Das Template an sich ist aktuell gerade mal 18 KB groß und besteht aus 10 Dateien (inkl. Bilddateien, exklusive Webfonts). Allerdings blähen die eingebetten Webfonts (EOT, SVG, TTF, WOFF und WOFF2) das ganz auf 1,9 MB auf. Bezüglich der CSS-Datei lässt sich vermutlich noch das eine oder andere KB einsparen, da viele Einträge nicht genutzt werden.

Was mir allerdings richtige Sorgen gemacht hat, war der Import der Wordpress-Artikel. Denn hier gibt es leider keine Erweiterung die unter Bolt CMS 3.x funktioniert. Ich habe mir daher ein abenteuerliche Lösung selbst gebaut. Leider hat diese aktuell noch dermaßen Ecken und Kanten, so dass ich vermutlich auch gleich die Artikel per Copy and Paste übertragen hätte können. Von der Entwicklungsdauer will ich erst gar nicht anfangen. Zudem sind bei einigen Artikeln Nachbesserungen nötig (spezielle Formatierungen von Wordpress-Erweiterungen usw.). Kurz gesagt, der Import war zum kotzen. Vermutlich wäre das aber auch so spaßig geworden, hätte ich auf ein anderes System gesetzt.

Ein weiteres Sorgenkind ist die Suchfunktion. Ich habe unter Bolt das Routing so geändert, dass die Links nicht https://planetlinux.de/entrie/deutschsprachiger-usenet-server-mit-schwerpunkt-arch-linux lautet sondern https://planetlinux.de/deutschsprachiger-usenet-server-mit-schwerpunkt-arch-linux. Dann zickt allerdings die Suchfunktion von Bolt. Allerdings bin ich mir nicht sicher, ob es wirklich an Bolt liegt oder ob ich hier das Problem bin. Hiermit werde ich die Entwickler von Bolt bzw. die Gemeinschaft um Bolt wohl noch mal um Hilfe bitten müssen. Alternativ überlege ich mir auch, ob ich überhaupt eine SuFu brauche...

Ansonsten läuft alles genauso wie ich es mir vorgestellt habe. Schnell, stabil und resourcenschonend. Im Debug-Modus werden gerade mal 2 MB in der Spitze verbraucht. Mein PHP Speicherlimit liegt bei 128 MB. Wenn ich den Debug-Modus deaktiviere, wird vermutlich noch weniger Speicher benötigt. Alles in allem war der Wechsel die richtige Entscheidung für mich. Vor allem wenn es um die Templates geht.
