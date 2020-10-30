---
title: Bitte sichert eure Daten
date: 2020-10-30T18:57:44+0100
categories:
- OSBN
- Linux
tags:
- Datensicherung  
slug: bitte-sichert-eure-daten
---
Vergangener Sonntag. Ich wollte eben etwas für ein neues Projekt machen für das ich die seit langem brach liegende Domain planetlinux.de nutzen will als ich einen Anruf erhalten habe.

Ein Kumpel von mir war sichtlich mit den Nerven am Ende. Datenverlust. Wichtige Daten. Was sonst?

Was ist passiert? Er hat sich eine neue Festplatte als Datengrab gekauft und diese mit luks / dm-crypt verschlüsselt und für ihn wichtige Daten darauf verschoben. Leider hat er wohl auch nachträglich an der Partition herumgespielt und dabei (wie auch immer) den Header gekillt ohne den eine Entschlüsselung nicht mehr möglich ist. Ich konnte also nicht helfen, da keine Datensicherung vorhanden war.

Daher möchte ich an dieser Stelle dazu aufrufen Backups zu machen.

Bei Verschlüsselungen mit luks / dm-crypt kann man mittels <mark>cryptsetup luksHeaderBackup --header-backup-file <file> <device></mark> (also zum Beispiel cryptsetup luksHeaderBackup --header-backup-file headerbak /dev/sda1) den Header der jeweiligen Partition sichern.

Das ist aber nur die halbe Miete. Auch eine HDD bzw. SSD kann defekt werden. Wenn es blöd läuft über Nacht. Daher sollte man auch zumindest seine wichtigen Daten regelmäßig sichern. Hierfür gibt es unzählige Programme. Ich nutze für Backups zum Beispiel [Borg](https://www.borgbackup.org), da die Daten damit von Haus aus verschlüsselt werden und dank der Deduplikation der Speicherbedarf bei neuen Backups sehr überschaubar ist. Lokal speichere ich die Datensicherungen auf bis zu zwei unterschiedliche Datenträger. Je nachdem wie wichtig sie sind.

Das ist aber noch nicht die ganze Miete. Denn solche Datensicherungen nützen wenig wenn das Haus abbrennt oder eingebrochen wird. Daher sollte man immer auch noch ein sogenanntes "off-side backup" seiner äußerst wichtigen Daten haben, das überall nur nicht im betreffenden Gebäude liegt. Ich nutze hierfür den Dienst [rsync.net](https://www.rsync.net) aus drei Gründen.

Zum einen weil es das Unternehmen schon länger gibt. Zum anderen weil der Speicherplatz für Nutzer von Borg [günstiger](https://www.rsync.net/products/borg.html) ist. Und weil offiziell empfohlen wird seine Daten vor dem Hochladen bitte selbst zu verschlüsseln.

Was aber nicht bedeuten soll, dass ihr die gleichen Tools nutzen sollt. Nutzt was ihr wollt. Nur macht bitte Backups eurer wichtigen Daten. Und zu einem Backup gehört auch, regelmäßig zu testen ob sich die Daten aus einem Backup wiederherstellen lassen.