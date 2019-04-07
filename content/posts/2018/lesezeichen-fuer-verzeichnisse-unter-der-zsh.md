---
title: Lesezeichen für Verzeichnisse unter der ZSH
date: 2018-01-07T18:06:00+0100
categories:
- Linux
- OSBN
tags:
- ZSH
- Lesezeichen
- Verzeichnisse
slug: lesezeichen-fuer-verzeichnisse-unter-der-zsh
---
Heute habe ich mir überlegt, wie ich meine Abläufe weiter optimieren kann. Der Wechsel in oft genutzte Verzeichnisse ist solch ein Ablauf. Als erstes habe ich mir das Jump-Plugin von Oh My ZSH angesehen.

Da mir Oh My ZSH zu überladen ist, habe ich mir nur das betreffende Plugin installiert. Hierzu habe ich das Verzeichnis /usr/share/zsh/plugins/zsh-jump erstellt und in diesem mittels wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/plugins/jump/jump.plugin.zsh das Plugin heruntergeladen. Abschließend habe ich noch in der ~/.zshrc source /usr/share/zsh/plugins/zsh-jump/jump.plugin.zsh hinzugefügt.

Das Plugin ist nun aktiv. Nun wechselt man einfach in eines der oft genutzten Verzeichnisse. Nehmen wir als Beispiel mal /etc/systemd/system. Mittels mark systemd legen wir ein Lesezeichen an (anstelle von systemd kann man eine beliebige Bezeichung angeben). Hiermit mit standardmäßig unter ~/.marks ein entsprechnender Symlink angelegt.

Nehmen wir nun einmal an, dass wir uns in ~/.config/terminator befinden und nun schnell in /etc/systemd/system wechseln möchten. Also führen wir jump systemd aus und landen umgehend in /etc/systemd/system.

Diese Lösung ist relativ einfach gehalten und erfordert das manuelle Anlegen von Lesezeichen. Andere Lösungen, die ich voraussichtlich noch testen werde, nutzen zum Beispiel fzf und sind daher komplexer und bietet mehr Möglichkeiten.
