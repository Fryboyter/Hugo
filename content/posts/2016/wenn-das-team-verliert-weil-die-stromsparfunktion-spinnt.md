---
title: Wenn das Team verliert weil die Stromsparfunktion spinnt
date: 2016-06-14T13:01:00+0100
categories:
- Allgemein
tags:
- Windows
- Stromsparfunktion
- Multiplayer
slug: wenn-das-team-verliert-weil-die-stromsparfunktion-spinnt
---
Stellt euch vor, ihr spielt gerade mit mehreren Leuten im Internet ein Spiel das Teamarbeit erfordert. Stellt euch weiterhin vor, das mitten im Spiel die Tastatur nicht mehr funktioniert. Stellt euch auch mal vor, dass man deswegen auch die eine oder andere Runde verliert. Dann wisst ihr wie genervt ich bis vor ein paar Tagen war.

Im Moment spiele ich eigentlich nur [Overwatch](https://playoverwatch.com/de-de "Overwatch"). Ein FPS in dem zwei Teams gegeneinander antreten. Wenn dann in Runde 5 nach zwei Minuten ein Teammitglied ausfällt weil seine Tastatur nicht mehr reagiert ist das ziemlich blöd. Noch blöder ist es, wenn man die Tastatur nur wieder zum laufen bekommen, wenn man entweder den Rechner neustartet oder unter den Tisch kriecht, den Stecker der Tastatur abzieht, bis drei zählt und ihn wieder ansteckt. Da ein Spiel in Overwatch in der Regel nur 5 Minuten dauert kann man das Spiel eigentlich abhaken. Das die eigenen Teammitglieder das nicht so toll finden, brauche ich vermutlich gar nicht erwähnen.

Auf der Suche nach dem Problem, welches ausschließlich unter Windows auftritt und nie unter Linux, habe ich die Ereignisanzeige durchgeackert. Nichts, was auf Eingabegeräte hinweist. Dann habe ich geschaut, ob Windows vielleicht die Tastatur (Ducky Shine 3) ausschalten darf um Energie zu sparen. Auch das war nicht der Fall. Zumal die Beleuchtung der Tastatur ja auch dann weiter geleuchtet hat, wenn das Problem aufgetreten ist. Ich habe Maus und Tastatur auf andere USB-Anschlüsse umgesteckt. Nach neuen Treibern gesucht. Die Firmware der Tastatur aktualisiert. Ich habe sogar die Platten auf Fehler überprüft (wieso auch immer. Zumindest habe ich so festgestellt, dass ein Datengrab wohl langsam erneuert gehört. Aber das ist ein anderes Thema).

Vor kurzem habe ich den Übeltäter erwischt. Im Gerätemanager sind bei mir einige USB-Root-Hubs aufgeführt. Und ratet mal, was hier die Standardeinstellung ist? Windows darf diese bei Bedarf ausschalten um Strom zu sparen. Scheinbar ist es Windows recht egal, wie ein angeschlossenes Gerät, welches über den USB-Root-Hub gesteuert wird, eingestellt ist. Denn nachdem ich (vorsorglich) allen USB-Root-Hubs die Erlaubnis entzogen habe, dass Windows diese ausschalten darf, funktioniert die Tastatur nun auch nach stundenlangem Spielen ohne Probleme.

Tja das Leben ist grausam und ungerecht. Und Windows trägt oft nicht dazu bei es zu verbessern.