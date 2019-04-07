---
title: Icons im Tray unter KDE Plasma 5 anzeigen
date: 2015-10-18T21:40:00+0100
categories:
- Linux
- OSBN
tags:
- Icons
- Tray
- KDE
- Plasma
- Xembed-sni-proxy
slug: icons-im-tray-unter-kde-plasma-5-anzeigen
---
Bisher wurden unter KDE 4.x die Icons im System Tray mittels xembed angezeigt. Plasma hingegen setzt nun auf SNI. Für viele Programme hatte das zu Folge, dass die Entwickler ihre Programm anpassen müssen. Bei einigen ist diese Anpassung bereits erfolgt. Bei anderen noch nicht. Bei einigen wird es vermutlich nie passieren. Und genau das ist ein Problem für viele Anwender.

Im Wiki von Arch Linux werden z. B. die Pakete sni-qt und libappindicator-gtk2 bzw. -gkt3 als Lösung angegeben. Bei mir hat bisher jede dieser Lösungen versagt. KeePass weigert sich beispielsweise auch nach der Installation besagter Pakete ein Icon anzuzeigen. Vermutlich weil Mono genutzt wird. Laut einem [Artikel](http://blog.davidedmundson.co.uk/blog/xembed_back) von David Edmundson, seines Zeichens Entwickler bei KDE, macht die Umstellung auf SNI bei den Nutzern größere Probleme als ursprünglich angenommen. Und zwar so große, dass nun [xembed-sni-proxy](https://github.com/davidedmundson/xembed-sni-proxy "xembed-sni-proxy") ins Leben gerufen wurde. Hiermit werden quasi "xembed-Icons" in "SNI-Icons" umgewandelt, so dass die Icons unter Plasma angezeigt werden.

Nach einem ersten Test ist das Projekt noch nicht wirklich ausgereift. In vielen Fällen wird beispielsweise ein leeres Icon angezeigt (Pidgin ist so ein Fall), so dass auf den ersten Blick einfach nur eine Lücke im System Tray zu sehen ist. Ein Klick auf diese Lücke öffnet aber das jeweilige Menü. Bei KeePass wird das Icon angezeigt. Nur lässt sich hier das Menü derzeit nur schließen wenn man einen Eintrag anklickt. Blöd wenn man das falsche Icon erwischt hat und das Menü einfach nur schließen will.

Edmundson hofft, dass xembed-sni-proxy in Plasma 5.5 Einzug halten kann. Diese Version ist für Dezember 2015 geplant, so dass bis dahin noch einige Zeit zum Beheben von Problemen bleibt. Wer nicht so lange warten will und zufällig Arch nutzt, findet im AUR das Paket xembed-sni-proxy-git.
