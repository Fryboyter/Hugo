---
title: Dauerhafte Lösung wenn ein Dienst die IP des VPN-Dienstes sperrt
date: 2018-01-04T16:30:00+0100
categories:
- Linux
- OSBN
tags:
- OpenVPN
- Route
slug: dauerhafte-loesung-wenn-ein-dienst-die-ip-des-vpn-dienstes-sperrt
---
Heute hat es mich mal wieder erwischt. Privat nutze ich aus diversen Gründen den Dienst eines VPN-Anbieters. Über die gleiche IP haben jetzt wohl Vollidioten Mist gebaut und einer meiner E-Mail-Anbieter hat diese für das Versenden gesperrt. Laut dem Support ist das Entsperren aktuell keine Option.

Vor längerem habe ich bereits einen [Artikel](https://fryboyter.de/ausnahme-fuer-openvpn-verbindung-erstellen) veröffentlich und beschrieben wie man eine Ausnahme bei OpenVPN erstellt. Da ich aber über die betreffende E-Mail-Adresse sehr selten etwas versende, werde ich mich vermutlich jedes mal wundern und erst einmal ein technisches Problem vermuten. Aber wie so oft, kann man das Problem auch dauerhaft lösen.

Hierzu editiert man einfach unter /etc/openvpn/client/ die betreffende Konfigurationsdatei und fügt folgenden Einträge hinzu.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">script-security 2
up /etc/openvpn/route.sh</code>
</pre>

Die erste Zeile erlaubt OpenVPN Nutzer-Scripte auszuführen. In der zweiten Zeile wird das Script route.sh ausgeführt, sobald die OpenVPN-Verbindung steht. Nimmt man anstelle von up down wird das Script ausgeführt, sobald die Verbindung beendet wurde. Was in dem Fall keinen Sinn machen würde. Im genannten Script ist dann folgendes Eintragen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/sh
route add -host mailserver.des.anbieters gw 192.168.1.1</code>
</pre>

Anstelle der genannten exemplarischen IP nimmt man einfach die IP des Routers (ich gehe davon aus, dass der VPN-Zugang nicht auf selbigen läuft, sondern auf dem Rechner(n).

Somit lassen sich die E-Mails ganz normal über die IP vom ISP empfangen oder versenden. Alles andere läuft weiterhin über den VPN-Zugang so dass man beispielsweise Geoblocking umgehen kann.
