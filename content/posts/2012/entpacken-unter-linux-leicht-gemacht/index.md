---
title: Entpacken unter Linux leicht gemacht
date: 2012-12-13T22:16:00+0100
categories:
- Linux
- OSBN
tags:
- Linux
- Archive
- Dtrx
- Alias
slug: entpacken-unter-linux-leicht-gemacht
---
Geht es euch auch so, dass ihr euch nicht merken könnt, mit welchen Parametern man z. B. ein tar-Archiv entpackt? Also mir schon. Deswegen habe ich mir unter der ZSH diverse Aliase angelegt (z. B. untar welcher tar -xvf ausführt) Heute habe ich eine Alternative dazu gefunden. [Dtrx](http://brettcsmith.org/2007/dtrx "Dtrx") (do the right extraction).

Das Tool entpackt zum Beispiel tar, zip, cpio, deb, rpm, gem, 7z, cab, lzh, rar, gz, bz2, lzma, xz, sowie diverse exe- und Installshield-Dateien und Windows-Cabinetdateien. Hierzu z. B. einfach dtrx test.tar ausführen und fertig. Die Dateirechte werden dabei so geändert, dass man als Nutzer lesend und schreibend auf die entpacktend Dateien zugreifen kann. Alle anderen Rechte bleiben unangetastet. Sollte sich ein Archiv im zu entpackendem Archiv befinden, wird dies auch mit entpackt. Die Verzeichnisstruktur wird beim Entpacken ebenfalls berücksichtigt.
