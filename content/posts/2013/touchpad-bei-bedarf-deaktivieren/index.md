---
title: Touchpad bei Bedarf deaktivieren
date: 2013-06-04T00:14:00+0100
categories:
- Linux
- OSBN
tags:
- Lenovo
- X130e
- Touchpad
slug: touchpad-bei-bedarf-deaktivieren
---
In letzter Zeit nutze ich immer öfter mein Netbook (Lenovo X130e) für alles mögliche. Allerdings erwische ich beim Tippen regelmäßig den Touchpad. Bei längeren Texten nervt das dann schon gehörig. Daher habe ich mir mal angesehen, wie ich den Touchpad bei Bedarf deaktivieren kann. Hierzu kann man den Befehl "xinput" nutzen.

Mittels "xinput list" erhält man eine Liste aller erkannten Eingabegeräte. Bei mir sieht das wie folgt aus:

{{< image src="xinput_touchpad.gif" alt="xinput_touchpad" >}}

Das Touchpad wird hier als "SynPS/2 Synaptics Touchpad" aufgeführt. Wichtig ist hier die ID des Gerätes. In diesem Fall 13.

Mittels "xinput --disable 13" kann man nun das Touchpad bei Bedarf deaktivieren. Um es wieder zu aktivieren reicht der Befehl "xinput --enable 13" aus.

Soll der Touchpad dauerhaft deaktiviert werden und das BIOS bietet keine Möglichkeit den Touchpad zu deaktivieren, kann man den Befehl in der Datei "~/.xinitrc" hinterlegen.
