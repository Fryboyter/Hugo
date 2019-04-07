---
title: Prüfsummen in einer PKGBUILD-Datei ändern
date: 2017-10-06T18:01:00+0100
categories:
- Linux
- OSBN
tags:
- PKGBUILD
- Prüfsumme
slug: pruefsummen-in-einer-pkgbuild-datei-aendern
---
Ab und zu kommt es vor, dass im AUR die PKGBUILD-Datei eines Pakets nicht aktualisiert wird. Das ist derzeit beim Editor micro der Fall, da es einen unschönen [Bug](https://github.com/zyedidia/micro/issues/779)mit der Mausunterstützung gibt und der Paketbetreuer erst mal abwarten will. Ich will aber nicht.

Bisher bin ich in solchen Fällen immer so vorgegangen, dass ich mir erst einmal die Prüfsumme des neuen Archivs besorgt habe. Bei einigen Programmen sind die aber entweder sehr gut versteckt oder werden gar nicht erst angeboten. Bei letzterem lade ich das neue Archiv ein- oder zweimal herunter und erstelle manuell die Prüfsumme. Dann lade ich mir mit curl die PKGBUILD-Datei herunter und editiere die Zeile pkgver= und dann noch die Zeile(n) für die Prüfsumme(n). Aber das nervt. Vor allem wenn man die Prüfsummen gar nicht oder nur schwer findet.

Aber wie soll es anders sein? Hätte ich mal in das Wiki von Arch Linux geschaut... Genau für diese Änderung gibt es das Tool updpkgsums, welches bei pacman direkt mit dabei ist. Hat man die PKGBUILD-Datei heruntergeladen und die Zeile pkgver= angepasst, muss man nur noch "updatepkgsums PKGBUILD" aufrufen. Das Tool ersetzt dann automatisch die alte gegen die neue Prüfsumme. Diese sollte man aber trotzden möglichst überprüfen. Wobei das in einigen Fällen eben nicht ganz leicht ist. Jetzt sollte man beispielsweise mittels "makepkg -i PKBUILD --noconfirm" die aktuelle Version des Programms installieren können.
