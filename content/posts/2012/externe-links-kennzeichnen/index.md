---
title: Externe Links kennzeichnen
date: 2012-09-23T17:45:00+0100
categories:
- Allgemein
tags:
- Internetseite
- Externe Links
slug: externe-links-kennzeichnen
---
<p>Gerade bin ich auf die Idee gekommen, hier die externen Links zu kennzeichnen. Also alle, die nicht unter fryboyter.de zu erreichen sind. Für Wordpress gibt es ein extra [Plugin](http://wordpress.org/extend/plugins/link-indication "Links indication") dafür. Allerdings kümmert sich scheinbar keiner mehr darum und noch ein Plugin wollte ich für die Angelegenheit nicht installieren. Von daher habe ich mal selbst Hand angelegt. Im Grunde genommen ist es recht einfach. Man öffnet einfach die Datei style.css (im jeweiligen Theme-Verzeichnis) mit einem Editor und fügt folgende Zeile ein und speichert die Datei wieder auf dem Webspace.

>a[href^=\"http://\"] { background: url(images/extern.png) right center no-repeat; margin-left: 1px; margin-right: 3px;padding-right: 16px;}

Nun fügt man noch in das Verzeichnis images innerhalb des jeweiligen Theme-Verzeichnis die Datei ein, mit der externe Links gekennzeichnet werden sollen. Bei diesem Beispiel habe ich sie extern.png genannt. Nun sollte jeder Link mit der Grafik versehen sein. Jeder? Ja, bisher jeder. Um wirklich nur externe Links zu markieren muss man noch folgende Zeile in die Datei style.css eintragen und die Datei wieder abspeichern.

>a[href^=\"https://fryboyter.de\"] { background: none; margin: 0; padding: 0;}

Anstelle von https://fryboyter.de muss man natürlich die eigene Domain, auf der Wordpress läuft, eintragen. Nun sollte jeder externe Link mit der Grafik markiert sein, interne jedoch nicht. Das Ergebnis kann man sich hier bei mir ansehen. Im Grunde genommen habe ich nichts anderes gemacht, als oben genanntes Plugin. Nur eben ohne extra Plugin.