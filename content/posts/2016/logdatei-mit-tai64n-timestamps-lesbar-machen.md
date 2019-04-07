---
title: Logdatei mit TAI64N-Timestamps lesbar machen
date: 2016-10-05T20:26:00+0100
categories:
- Linux
- OSBN
tags:
- Logdatei
- Tai64n
- tai64nlocal
slug: logdatei-mit-tai64n-timestamps-lesbar-machen
---
Ich habe hier eine Logdatei bei der jede Zeile mit einer Zahlenreihenfolge beginnt. Nach etwas Recherche habe ich herausgefunden, dass es sich um TAI64-Timestamps handelt. 4611686018427387904 entspricht hier z. B. dem 01.01.1970 01 Uhr.

Um diesen Timestamp lesbar zu machen, kann man sich des Tools tai64nlocal bedienen. Man findet es im Paket daemontools.

Mittels z. B. **cat $logdatei | tai64nlocal | less** schickt man mit cat die Logdatei an tai64nlocal und lässt sich dann den umgewandelten Inhalt mit less anzeigen.
