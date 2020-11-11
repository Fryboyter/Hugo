---
title: KrISS feed - (m)eine Alternative zu Tiny Tiny RSS?
date: 2013-09-25T09:48:00+0100
categories:
- OSBN
- Allgemein
tags:
- KrISS
- Feed
- Reader
slug: kriss-feed-meine-alternative-zu-tiny-tiny-rss
---
Seit einiger Zeit, genauer seit Google Reader dicht gemacht wurde, nutze ich Tiny Tiny RSS als Ersatz, da ich dies selbst hosten kann und nicht auf Dritte angewiesen bin. Funktioniert Tiny Tiny RSS? Ja. Bin ich damit zufrieden? So ziemlich. Nun kommt aber das große Aber... Ich mag die Art des Entwicklers, dass er in seinem Forum an den Tag legt nicht. Und viele der dort registrierten Nutzer schlagen in die gleiche Kerbe. Von daher sehe ich mir regelmäßig Alternativen an, die ich auch selbst hosten kann. Gestern bin ich mal wieder auf eine gestoßen, die Tiny Tiny RSS bei mir vermutlich ablösen wird. Meine Entdeckung hört auf den Namen [KrISS feed](http://tontof.net/kriss/feed "KrISS feed"). Dieser Reader benötigt nur php 5.2, curl, libxml2 und mbstring. Eine Datenbank ist nicht nötig. Und er besteht aus genau einer PHP-Datei. Plugins sind ab der derzeit aktuellen Version auch möglich, aber bisher noch nicht vorhanden. Hier gibt es auf jeden Fall noch Nachholbedarf. So vermisse ich derzeit auch die Filterfunktion um gewisse Artikel eines Feeds automatisch zu löschen. Dies ist für mich wichtig, da bei einigen Feeds Teilnehmer mehr auf Masse statt auf interessante Artikel setzen. Oder mich einfach gewisse Themen eines Feeds an sich nicht interessieren.

Optisch sagt er mir auch zu. Wer will kann per CSS die Optik auch selbst anpassen bzw. vorhandene Themes nutzen.

{{< image src="ali0une_white.jpg" alt="KrISS feed" >}}

Da der Reader bisher nur in Französisch und Englisch erhältlich ist, habe ich gestern angefangen eine deutsche Version zu erstellen. Mit der einen oder anderen Übersetzung habe ich allerdings noch Probleme, da einige Stellen in einem ziemlich komischen Englisch gehalten sind und ich schlicht und ergreifend keine Ahnung habe, was gemeint ist. Vermutlich ist die Muttersprache des Entwicklers Französisch und sein Englisch nicht unbedingt einwandfrei. Und ich noch nicht so vertraut mit dem Programm. Und im Reader direkt kann man die Sprache bisher auch noch nicht auf Deutsch umstellen. Derzeit funktioniert nur der direkte Aufruf über http://rss.domain.de/?lang=de_DE. Wer die derzeitige deutsche Version testen will, kann sich gerne bei mir melden, dann schicke ich ihm/ihr die Datei zu. Sobald ich mit der Übersetzung fertig bin, werde ich diese dem Entwickler zukommen lassen (hoffen wir mal dass dieser etwas anders tickt). Nur wegen der Sprache zur forken ist mir dann doch zu blöd. Wer mit Französisch oder Englisch kein Problem hat, kann sich unter [http://tontof.net/feed/](http://tontof.net/feed "KrISS feed Demo") auch eine Demoinstallation ansehen. Hier hat man allerdings nur Gastrechte.
