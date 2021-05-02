---
title: WLAN-USB-Stick Cudy WU1300S unter Linux
date: 2021-05-02T16:49:00+0200
categories:
- OSBN
- Linux
tags:
- WLAN
- USB
slug: wlan-usb-stick-cudy-wu1300S-unter-linux
---
Kürzlich habe ich einen günstigen und kompakten WLAN-USB-Stick benötigt. Spontan habe ich mir den WU1300S der Firma Cudy gekauft.

Laut den technischen Daten erreicht der Stick bis zu 400 Mbit in einem 2,4 GHz WLAN und 867 Mbit in einem 5 Ghz WLAN. Die Abmessungen betragen 37,5 x 17 x 8,5 Milimeter. Verbaut ist der rtl88x2bu Chipsatz von Realtek. Neben Windows und MacOS wird offiziell auch Linux unterstützt.

Nach dem Einstecken des Sticks in einen USB-Port wurde der Stick allerdings unter Arch Linux nicht gefunden. Es ist somit kein WLAN-USB-Stick der "out of the box" funktioniert.

Um ihn nutzen zu können, muss man den Treiber der [hier](https://github.com/cilynx/rtl88x2bu) angeboten wird, installieren. Wer Arch Linux nutzt, findet im AUR ein entsprechendes [Rezept](https://aur.archlinux.org/packages/rtl88x2bu-dkms-git/), das DKMS nutzt.

Damit funktioniert der Stick zufriedenstellend. Zumindest auf den ersten Blick. Denn nachdem der betreffende Rechner in den Energiesparmodus (suspend) versetzt und dann wieder aufgeweckt wird, wird die Netzwerkverbindung nicht mehr neu aufgebaut. Die Lösung ist allerdings recht einfach. In die Datei /etc/wpa_supplicant/wpa_supplicant.conf trägt man einfach <mark>ap_scan=1</mark> ein. Die Dokumentation hierfür lautet wie folgt.

>wpa_supplicant initiates scanning and AP selection; if no APs matching to the currently enabled networks are found, a new network (IBSS or AP mode operation) may be initialized (if configured) (default)

Von nun an funktioniert die WLAN-Verbindung problemlos. Positiv anzumerken ist auch, dass der Stick überhaupt nicht warm wird. Dafür das ich bis vor einigen Tagen die Firma Cudy, die übrigens aus China kommt, nicht kannte, kann ich den Stick unterm Strich empfehlen. Vor allem weil er beispielsweise mit aktuell 12,90 Euro nur einen Bruchteil des von mir bereits vorgestellten WLAN-USB-Sticks [AC 860](/fritz-wlan-stick-ac-860-unter-linux/) von AVM kostet.