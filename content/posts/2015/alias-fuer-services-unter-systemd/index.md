---
title: Alias für Services unter systemd
date: 2015-04-30T22:56:00+0100
categories:
- Linux
- OSBN
tags:
- Alias
- Systemd
- Service
slug: alias-fuer-services-unter-systemd
---
Manche Services unter systemd haben ziemlich umständliche Bezeichnungen. Systemd-networkd.service oder openvpn@vpn.service zum Beispiel. Um es sich beim Aktivieren, Deaktivieren oder Neustarten etwas einfacher zu machen, kann man hier zu einem Alias greifen. Nehmen wir mal openvpn@vpn.service als Beispiel.

Hier öffnet man einfach die Datei openvpn@vpn.service welche unter /etc/systemd/systemd/multi-user.target.wants/ liegt. Diese sollte wie folgt aussehen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Unit]
Description=OpenVPN connection to %i 

[Service]
Type=forking
ExecStart=/usr/bin/openvpn --cd /etc/openvpn --config /etc/openvpn/%i.conf --da$ 
PIDFile=/run/openvpn@%i.pid 

[Install]
WantedBy=multi-user.target</code>
</pre>

Soll der Service auf den Alias vpn1 reagieren, muss man einfach unter [Install] Alias=vpn1.service hinzufügen. Wichtig ist hier, dass der Alias die gleiche Endung hat wie das Original. Also in dem Fall .service. Hier kann man auch mehrere Aliase angeben, welche man in die gleiche Zeile mit einem Lehrschritt getrennt eingibt.

Hat man die Datei nun entsprechend geändert und abgespeichert aktiviert man den Service mittels systemctl enable openvpn@vpn.service. Hiermit wird nun ein Symlink vpn1.service angelegt, welcher auf openvpn@vpn.service verweist. Von nun an kann dieser "Service" anstelle des Originals genutzt werden. Also beispielsweise systemctl status vpn1.service.
