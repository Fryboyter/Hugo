---
title: Rclone - Daten mit mehreren Cloud-Anbietern synchronisieren
date: 2018-08-11T10:07:00+0100
categories:
- Linux
- OSBN
tags:
- Rclone
- Synchronisation
slug: rclone-daten-mit-mehreren-cloud-anbietern-synchronisieren
---
Wie nun [bekannt wurde](https://linuxnews.de/2018/08/dropbox-verprellt-linux-anwender/?utm_source=feedburner&amp;utm_medium=feed&amp;utm_campaign=Feed%3A+linuxnewsde+(linuxnews.de)), wird der Cloud-Anbieter Dropbox demnächst unter Linux nur noch Daten auf unverschlüsseltem ext4-Dateisystem synchronisieren. Bisher hatte ich dort meine verschlüsselten Datenbank-Dumps hochgeladen. Allerdings werde ich wegen einem Programm definitiv nicht von Btrfs auf ext4 umsteigen.

Da ich die Daten weiterhin gerne "offside" speichern und diese dann mit einem meiner Rechner herunterladen würde, habe ich mich spontan für pCloud als Alternative entschieden. Diesen Dienst nutze ich schon seit längerem ohne Probleme unter Linux und Windows. Zudem hat dieser seinen Sitz in der Schweiz und nicht in den USA. Für die Sicherung auf Dropbox hatte ich bisher den [Dropbox-Uploader](https://github.com/andreafabrizi/Dropbox-Uploader) genutzt. Ein solches einzelnes Script gibt es scheinbar für pCloud nicht. Ist wohl nicht bekannt genug. Nach etwas Google-Fu bin ich allerdings auf [rclone](https://rclone.org)gestoßen. Mit diesem Tool lassen sich Daten mit diversen Cloud-Anbietern aber auch über SFTP, HTTP oder WebDAV synchronisieren.

Die Einrichtung von rclone ist dank der Dokumentation ein Kinderspiel. Im Grunde reicht es die Binärdatei rclone herunterzuladen und rclone config auszuführen. Hierbei wird dann das eine oder andere abgefragt, was aber kein größeres Problem darstellt. Alles in allem dürfte die Umstellung von Dropbox-Uploader auf rclone inkl. lesen der Dokumentation und Anpassung des Backup-Scripts keine 10 Minuten gedauert haben. Wer also auch von Dropbox weg will, sich aber kein eigene Upload-Script bauen will, sollte sich rclone einmal ansehen. Das Tool ist übrigens unter der MIT Lizenz veröffentlicht und das Projekt gibt es seit ca. 6 Jahren und wird aktiv weiterentwickelt. Somit sollte es auch in absehbarer Zeit noch funktionieren.
