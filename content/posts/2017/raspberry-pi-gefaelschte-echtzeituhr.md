---
title: Raspberry Pi - Gefälschte Echtzeituhr
date: 2017-03-18T23:11:00+0100
categories:
- Linux
- OSBN
tags:
- Raspberry Pi
- Echtzeituhr
slug: raspberry-pi-gefaelschte-echtzeituhr
---
Da die Raspberry Pi nicht mit einer Echtzeituhr ausgerüstet sind, stellt dich das Datum nach jedem Reboot erst einmal auf den 01.01.1970 00:00 Uhr.

Wer seinem Raspberry kein RTC-Modul (z. B. DS3231) spendieren möchte und es mit der Zeit nicht ganz so genau nimmt, kann schummeln und sich fake-hwclock installieren. Hiermit wird die aktuelle Uhrzeit des Raspberry Pi periodisch sowie beim Herunterfahren in eine Datei gespeichert und beim Booten wiederhergestellt. In Verbindung mit einem NTP-Client lässt sich so die Uhrzeit des Raspberry Pi durchgehend halbwegs aktuell halten.
