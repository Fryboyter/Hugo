---
title: Gajim - Nachricht beim Betreten und Verlassen eines MUC deaktivieren
date: 2017-05-25T19:38:00+0100
categories:
- OSBN
tags:
- Gajim
- XMPP
- OSBN
slug: gajim-nachricht-beim-betreten-und-verlassen-eines-muc-deaktivieren
---
Martin von mdosch.de hat gestern einen Multi-User-Chat für das OSBN [erstellt](https://blog.mdosch.de/2017/05/24/osbn-chat). Der Idee an sich nicht abgeneigt, habe ich mich gestern und heute dort mit dem Client Gajim eingeloggt. An einer Stelle nervt das Teil aber.

Jedes mal wenn jemand den Chat betritt oder verlässt wird eine entsprechende Nachricht angezeigt. Das nervt. Also allgemein und nicht nur beim OSBN-MUC. Eine Möglichkeit dies über die normalen Einstellungen zu deaktivieren habe ich nicht gefunden. Daher habe ich ein paar Minuten einfach mal die Suchmaschine meiner Wahl gequält und bin fündig geworden...

Wenn man die Einstellungen von Gajim aufruft findet man ganz rechts den Reiter "Erweitert". Dort findet man dann ganz unten den "erweiterten Konfigurationseditor". Dort muss man dann nach print_status_in_muc suchen und dort bei Wert none eintragen. Und schon hält Gajim die Klappe wenn jemand den MUC verlässt oder betritt.