---
title: Dropbox vernünftig mit einem TrueCrypt-Container verwenden
date: 2009-12-31T15:23:00+0100
categories:
- OSBN
- Allgemein
tags: 
- TrueCrypt
- Dropbox
- Sync
slug: dropbox-vernuenftig-mit-einem-truecrypt-container-verwenden
---
[https://www.dropbox.com/](https://www.dropbox.com/ "Dropbox") ist ja eigentlich eine schöne Sache, um von unterschiedlichen Lokalitäten (nein damit sind keine Kneipen gemeint) auf diverse Daten zuzugreifen. Oder um einfach gewisse Daten außerhalb des Rechners zu sichern. Da aber die Verschlüsselung auf der Seite des Anbieters läuft, bin ich mit solchen Diensten immer sehr vorsichtig. Man kann auch sagen leicht paranoid. Der Einsatz eines TrueCrypt-Containers wäre zwar kein Problem, aber oft wird dann bei einer Aktualisierung immer die gesamte Datei neu hochgeladen und nicht nur die Änderungen. Das kann bei einer geringen Uploadgeschwindigkeit und 2 GB schon mal etwas dauern. Laut dem Dropbox-Client sind es bei mir noch 8 Stunden (weshalb ich das ganze lieber auf morgen verschoben habe. Bin heute Abend ja nicht daheim und deswegen ist der Rechner aus).

Soeben habe ich aber die Lösung gefunden. Caschy beschreibt in seinem [Blog](http://stadt-bremerhaven.de/dropbox-und-truecrypt-verschluesselte-daten-in-der-cloud/trackback/ "Blog") eigentlich sehr gut, wie man das Problem bei der Aktualisierung der Containerdatei umgehen kann. Im Grunde ist es eigentlich ganz einfach. Nur muss man es halt erst einmal wissen. Aber lest selbst.

Bei der Linuxversion nennt sich der Punkt im übrigen "Preserve modification time of file containers".

Ich werde das ganze morgen mal etwas genauer testen. Zum Hochladen eines 2 GB Containers fehlt mir heute die Zeit. Und auf einen kleineren Container habe ich keine Lust.