---
title: Ausnahme für OpenVPN-Verbindung erstellen
date: 2013-03-02T22:52:00+0100
categories:
- Linux
- OSBN
tags:
- Ausnahme
- OpenVPN
slug: ausnahme-fuer-openvpn-verbindung-erstellen
---
Ich nutze privat einen VPN-Dienst. Derzeit ovpn.to um genau zu sein. Auf manchen Seiten ist das aber ein Nachteil, da manche Vollpfosten solche Dienst zum Spammen usw. missbrauchen und der Seitenbetreiber die IP sperrt. So bleiben im Grunde zwei Möglichkeiten. Entweder man deaktiviert die VPN-Verbindung komplett oder man besucht die Seite nicht mehr. Oder man nimmt Möglichkeit drei und erstellt eine Ausnahme. Unter OpenVPN und Linux reicht hier ein einfacher Befehl.

>route add -host heise.de gw 192.168.1.1

Hier wird eine Route erstellt mit der alle Anfragen die an heise.de gehen über den Gateway mit der IP 192.168.1.1 (in dem Fall der Router) gehen und nicht über die VPN-Verbindung. Alles andere läuft weiterhin über die VPN-Verbindung. Will man nun das Ganze wieder löschen muss man einfach den Befehl wiederholen, nur dass man anstelle add del angibt.

>route del -host heise.de gw 192.168.1.1

Sollte jemand eine bessere Möglichkeit kennen, immer her damit. So kann man übrigens auch weiterhin die SMTP-Server nutzen, welche in der Regel auch allergisch auf VPN-Dienste reagieren.
