---
title: Temperatur des Raspberry Pi auslesen
date: 2015-07-05T13:55:00+0100
categories:
- Linux
- OSBN
tags:
- Raspberry Pi
- Temperatur
slug: temperatur-des-raspberry-pi-auslesen
---
Bei den aktuellen Temperaturen wollte ich mal wissen, wie sich hier mein Raspberry Pi schlägt, da dieser in einem nicht gerade kühlen Raum läuft. Dies kann man mit Boardmitteln auslesen und muss kein extra Paket installieren.

Unter /opt/vc/bin findet man den Befehl vcgencmd. Ruft man diesen mittels vcgencmd measure_temp auf, bekommt man die Temperatur des SoC angezeigt. Bei mir liegt diese aktuell bei 44,4 Grad Celsius. Für den Raspberry Pi ist das absolut in Ordnung. Erst ab 80 Grad Celsius wird es kritisch. Bei 85 zieht der Raspberry Pi automatisch die Notbremse und setzt den Takt herunter.
