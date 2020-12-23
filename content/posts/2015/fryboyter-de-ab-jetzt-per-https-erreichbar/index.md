---
title: Fryboyter.de ab jetzt per https erreichbar
date: 2015-12-05T20:13:00+0100
categories:
- Linux
- OSBN
tags:
- Fryboyter
- HTTPS
slug: fryboyter-de-ab-jetzt-per-https-erreichbar
---
Es ist vollbracht. Fryboyter.de läuft nun dank Let's Encrypt mit https. Die Anleitung von Uberspace der ich gestern bereits einen [Artikel](/offizielles-vorgehen-bei-uberspace-mit-lets-encrypt/) gewidmet habe, hat einwandfrei funktioniert. Danach war allerdings noch die eine oder andere Anpassung nötig. Hauptsächlich an Wordpress.

Als erstes habe ich im Backend von Wordpress unter den allgemeinen Einstellungen die Wordpress- sowie Website-Adresse von http://fryboyter.de auf https://fryboyter.de geändert. Danach lies sich schon einmal die Seite an sich verschlüsselt aufrufen. Aber irgend etwas hat nicht gepasst.

Ich markiere alle externen Links mit einem kleinen Symbol wie ich [hier](/externe-links-kennzeichnen/) schon beschrieben habe. Da die Seite nun per https aufgerufen wird, hat das ganze nun auch alle internen Link gekennzeichnet. Also schnell die Ausnahme von der Kennzeichnung auf https://fryboyter.de geändert. Soweit so gut. Piwik wurde auch noch unverschlüsselt eingebunden. Also auch hier schnell den Tracking-Code auf https geändert, welcher bei mir in der Datei footer.php eingetragen ist.

War es das? Leider nein. Leider war bei alle Grafiken die ich über die Mediathek von Wordpress eingebunden habe noch http eingetragen. Warum wurde das nicht bei der Änderung in den allgemeinen Einstellungen mit geändert? Eine globale Änderung der Mediathek-Links über das Backend ist scheinbar auch nicht vorgesehen. Püh... Was nun? Ich habe mich dann kurzerhand einfach mal mit der Datenbank verbunden und mir die diversen Tabellen angesehen. Dabei ist mir aufgefallen, dass ich in einigen Artikeln auch noch auf andere Artikel verwiesen habe. Natürlich per http://. Ja leck mich doch. Also habe ich mir eine SQl-Anweisung gebaut, die nach http://fryboyter.de sucht und alle Treffer in der Datenbank durch https://fryboyter.de ersetzt. Diese werde ich an dieser Stelle erst mal nicht veröffentlichen. Nicht dass ich hier irgendwo Mist gebaut habe. Zudem sollte es mit [diesem](https://github.com/interconnectit/Search-Replace-DB) Tool wohl auch einfacher gehen. Da es quelloffen ist, sollte es auch keine Hintertürem haben oder Zugangsdaten abgreifen. Meine Hand lege ich aber definitiv nichts ins Feuer dafür. Das Teil habe ich natürlich erst hinterher gefunden und daher in keinster Weise getestet.

Nun aber, oder? Nicht ganz. Fryboyter.de ist weiterhin per http erreichbar. Also noch schnell die htaccess-Datei für Wordpress angepasst, dass immer die Seite per https aufgerufen wird. Hier habe ich mich einfach im Blog von Überspace [bedient](https://wiki.uberspace.de/webserver:htaccess#https_erzwingen) und die "schickere" Variante gewählt. Auch wenn diese wohl bei älteren Browsern Probleme macht. Da hier aber hauptsächlich Besucher mit aktuellen Versionen aufschlagen sollte es nicht wirklich ein Problem sein.

Das sollte es dann aber wirklich gewesen sein. Wenn ich doch irgendwo etwas übersehen habe, wäre ich über einen Hinweis nicht unglücklich.

Abschließen kann ich nur feststellen dass das Beantragen und Einbauen des Zertifikats in deutlich weniger als 5 Minuten erledigt war. Auch das Scharfschalten ging ratz fatz. Die ganzen Anpassungen an der Seite an sich haben dann aber doch länger gedauert. Vor allem der Mist mit der Mediathek und den Links in den Artikeln...
