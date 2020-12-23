---
title: Kurztest TP-Link WN722NC WLAN-USB-Stick
date: 2015-01-03T22:16:00+0100
categories:
- Linux
- OSBN
tags:
- TP-Link
- WN722NC
- Kurztest
slug: kurztest-tp-link-wn722nc-wlan-usb-stick
---
Manchmal nervt mich WLAN. Manchmal könnte man denken, der Teufel hätte es erfunden. Zumindest wenn man zum einen Linux nutzt und zum anderen so ein saudummes Netbook hat, dessen Hersteller zum einen eine WLAN-Karte von Broadcom verbaut und zum anderen im Bios eine Whitelist einbaut (welche er natürlich nicht veröffentlicht), wegen der dann nur gewisse Netzwerkkarten verbaut werden können. Karten von Intel gehören scheinbar nicht dazu, sonst wäre das Thema schon lange erledigt. Da Intel scheinbar keine WLAN-Sticks herstellt, habe ich (wie bereits [geschrieben](/mein-netbook-ist-endlich-broadcom-frei/)) die WLAN-Karte deaktiviert und bin auf einen kleinen USB-Stick mit Realtek-Chipsatz umgestiegen, welcher mit dem Modul rtl8192cu unter Linux genutzt werden kann. Zumindest bis vor ein paar Tagen.

Urplötzlich hatte ich nach einem Update alle paar Minuten einen kompletten Absturz des Sticks. Keine Internetverbindung, kein Pingen des Routers. Nichts. Ein Neustart der Netzwerkverbindung hat das Problem beseitig, welches dann nach ein paar Minuten wieder aufgetreten ist. Laut diversen Treffern bei Google bin ich hier nicht alleine betroffen. Bei vielen hat ein Downgrade des Pakets linux-firmware geholfen. Bei mir natürlich nicht. Hätte mich auch gewundert.

Wie es der Zufall so will, habe ich für einen Bekannten zwei WLAN-Sticks (TP-Link WN722NC) bestellt welche er noch nicht abgeholt hat. Die Sticks laufen mit Atheros-Chipsätzen. Die hatte ich bisher am Netbook noch nicht... Also mal eben meinen Bekannten angerufen und grünen Licht erhalten und somit einen der Sticks ausgepackt. An Hardware wird der Stick an sich, eine Antenne (welche man an den Stick schrauben kann um die Leistung zu verstärken) sowie eine Docking-Station mitgeliefert.

{{< image src="k-IMG_20150103_191826.jpg" alt="k-IMG_20150103_191826.jpg" >}} {{< image src="k-IMG_20150103_191746.jpg" alt="k-IMG_20150103_191746.jpg" >}}

Für ein Netbook ist der Stick ein ziemlicher Brocken (93,5mm*26mm*11mm). Vor allem wenn auch noch die Antenne angeschraubt ist. Beim Transport würde ich den Stick definitv entfernen.

Angesprochen wird der Stick unter Linux über das Modul ath9_htc. Bisher läuft der Stick hiermit stabil seit einigen Tagen und ist laut Router (OpenWRT) mit 120 Mbps angebunden. Wenn man sich so in diversen Wardriving-Foren umsieht, wird dort dieser Stick auch sehr oft empfohlen. Und das schon seit längerem. Da der Stick aktuell für etwas unter 8 Euro zu haben ist, kann ich hier aktuell nur eine Empfehlung aussprechen. Mal sehen ob bzw. wann ich das bereue. Das nächste Net- bzw. Notebook wird definitv eines mit einer WLAN-Karte von Intel bzw. eines ohne White- bzw. Blacklist. Oder eines für das man ein modifiziertes Bios erhält...
