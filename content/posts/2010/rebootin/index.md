---
title: Rebootin
date: 2010-04-03T22:07:00+0100
categories:
- Linux
- OSBN
tags:
- Rebootin
- Grub
- Bootloader
- Neustart
slug: rebootin
---
Hauptsächlich verwende ich ja Mandriva als Betriebssystem. Ab und zu kommt es allerdings vor, dass ich auch mal Windows 7 booten muss. Zum Beispiel zum Zocken. Das geht unter Windows einfach besser.

Bei einem Neustart muss ich dann allerdings immer den gewünschten Eintrag in Grub auswählen. Eigentlich kein Ding, aber es nervt doch irgendwie. Gerade wenn man öfters mal Windows starten muss. Vor einiger Zeit bin ich auf "Rebootin" gestoßen. Damit kann unter Mandriva (und vermutlich jeder anderen Linuxdistribution) Grub mitteilen, welchen Eintrag aus der menu.lst gestartet werden soll.

Mit **rebootin -l** kann man sich die Einträge aus der menu.lst anzeigen lassen. Bei mir wird zum Beispiel folgendes angezeigt:

>linux linux-nonfb failsafe windows

Mittels **rebootin windows** wird Mandriva heruntergefahren und Windows automatisch gestartet. So lassen sich recht einfach kleine Scripte anlegen, mit denen man die gewünschten Einträge booten kann.

Ich würde das jetzt nicht als "must have" einordnen, aber in manchen Situationen ist das doch irgendwie recht angenehm.

Rebootin ist übrigens Bestandteil des Paketes "bootloader-utils". Zumindest unter Mandriva.
