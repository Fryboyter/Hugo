---
title: Netctl funktioniert wegen Abhängigkeit von powerdevil nicht mehr
date: 2016-07-13T09:40:00+0100
categories:
- Linux
- OSBN
tags:
- Netctl
- Abhängigkeit
- Powerdevil
slug: netctl-funktioniert-wegen-abhaengigkeit-von-powerdevil-nicht-mehr
---
Vor ein paar Tagen habe ich KDE Plasma 5.7 unter Arch Linux auf meinem Notebook installiert. Nach einem Neustart konnte ich keine Verbindung mit dem WLAN aufbauen. Egal was ich versucht habe, der Service von netctl konnte nicht gestartet werden.

Nach einigen Minuten habe ich festgestellt, dass der Service von NetworkManager läuft. Frage 1. Warum läuft NetworkManager? Frage 2. Warum ist das Teil überhaupt installiert? Die zweite Frage konnte ich schnell beantworten. PowerDevil (ein Dienstprogramm unter KDE Plasma welches für die Energieverwaltung für Notebooks usw. zuständig ist), hat nun die fixen Abhängigkeiten networkmanager und networkmanager-qt. Frage 1 ist schon schwieriger. Wenn ich mittels systemctl stop NetworkManager.service Networkmanager stoppe kann ich eine WLAN-Verbindung mit netctl aufbauen. Ok, dann eben noch ein systemctl disable NetworkManager.service um den Dienst zu deaktivieren. Neustart... Netctl kann keine Verbindung aufbauen. Ah ja... Ein systemctl status NetworkManager.service zeigt mir, dass NetworkManager läuft. Ok... Scheinbar "braucht" irgendein anderer Service NetworkManager (wenn er installiert ist) und aktiviert mal eben ganz frech den Service wieder. Da ich an dieser Stelle keine Lust mehr hatte und reichlich genervt war, habe ich die Keule ausgepackt und den Service von NetworkManager kurzerhand mittels systemctl mask NetworkManager.service maskiert. Das hat zu folge, dass man den Dienst gar nicht mehr starten kann. Auch nicht von Hand. Hierfür müsste ich die Maskierung erst wieder entfernen. Ist mir aber auch egal. Ich mag NetworkManager nicht und PowerDevil funktioniert bei mir auch ohne NetworkManager.

Ich hoffe mal, dass die Entwickler von PowerDevil ein Einsehen haben, und NetworkManager als feste Abhängigkeit entfernen. Wegen mir kann das Zeug ja als optionale Abhängigkeit bestehen bleiben. Irgendeinen Sinn wird NetworkManager bei PowerDevil ja haben.
