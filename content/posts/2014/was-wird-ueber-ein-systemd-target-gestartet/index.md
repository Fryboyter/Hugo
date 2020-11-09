---
title: Was wird über ein systemd-target gestartet?
date: 2014-12-08T15:42:00+0100
categories:
- Linux
- OSBN
tags:
- Systemd
- Target
slug: was-wird-ueber-ein-systemd-target-gestartet
---
Systemd bietet sogeannte Targets. Grob gesagt so etwas wie Runlevel wie man sie von sysVinit her kennt. Multi-user.target entspricht hier am ehesten Runlevel 3. Graphical.target Runlevel 5. Um sich eine Übersicht zu verschaffen welche Services zum Beispiel das Target multi-user.target ausführen möchte, kann man folgenden Befehl verwenden:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">systemctl show -p "Wants" multi-user.target</code>
</pre>

Als Ergebnis erhält man dann beispielsweise folgende Ausgabe:<

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">Wants=cronie.service openvpn@nvpn.service unbound.service remote-fs.target systemd-networkd.service
haveged.service updatedb.timer shadow.timer rpcbind.service logrotate.timer man-db.timer
nsystemd-logind.service systemd-user-sessions.service getty.target systemd-ask-password-wall.path
ndbus.service</code>
</pre>

Anstelle von Wants kann auch WantedBy, Requires, RequiredBy, Conflicts, ConflictedBy, Before, After genutzt werden. Eine genauere Erklärung der sogenannten Section Options findet man [hier](http://www.freedesktop.org/software/systemd/man/systemd.unit.html). Daher gehe ich hier nicht näher darauf ein.
