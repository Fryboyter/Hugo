---
title: Entferntes Verzeichnis über SSH lokal mounten
date: 2012-08-24T19:52:00+0100
categories:
- Linux
- OSBN
tags:
- Verzeichnis
- SSH
- Mounten
- Sshfs
slug: entferntes-verzeichnis-ueber-ssh-lokal-mounten
---
Ich arbeite recht oft mit SSH um auf andere Rechner zuzugreifen. Ab und zu finde ich es recht angenehm, wenn ich ein Verzeichnis, dass eigentlich auf einem Server liegt, lokal mounten kann. Mit sshfs ist das kein Problem.

Erst einmal erstellt man sich auf dem Rechner vor dem man sitzt an einer Stelle an der man Lese- und Schreibzugriff hat ein Verzeichnis. Am besten im eigenen Home-Verzeichnis.

>mkdir sshfs

Das Verzeichnis muss nicht zwangsläufig sshfs heißen. Einfach einen Namen angeben, mit dem man etwas anfangen kann.

Nun muss man eigentlich nur noch das gewünschte Verzeichnis des entfernten Rechners in dieses Verzeichnis mounten. Hierzu reicht ein recht simpler Befehl.

>sshfs $Benutzername@$Rechner:/Verzeichnis/auf/dem/Rechner sshfs

Bei $Benutzername muss man den Benutzernamen angeben, mit dem man sich auf dem entfernten Rechner mit SSH einloggen kann. $Rechner ist der Name/IP des entfernten Rechners. Und /Verzeichnis/auf/dem/Rechner ist eben das Verzeichnis auf dem entfernten Rechner, dass man lokal mounten will. Sshfs ist das Verzeichnis, dass wir gerade eben lokal angelegt haben.

Wechselt man nun in das lokal angelegte Verzeichnis findet man dort den Inhalt des entfernten Verzeichnisses vor und kann damit arbeiten, wie wenn alles lokal vorhanden wäre. Nur mit einer kleinen Ausnahme. Es gibt oft eine kleine Verzögerung, wenn man z. B. in ein Unterverzeichnis wechselt.

Aushängen kann man das Verzeichnis wieder, in man einfach folgenden Befehl absetzt.

>fusermount -u ~/sshfs
