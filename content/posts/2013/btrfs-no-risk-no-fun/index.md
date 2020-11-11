---
title: Btrfs - no risk no fun
date: 2013-07-06T15:04:00+0100
categories:
- Linux
- OSBN
tags:
- Btrfs
- Dateisystem
- Risk
- Fun
slug: btrfs-no-risk-no-fun
---
Ich verfolge die Entwicklung von Btrfs, dem zukünftigen Linux-Filesystem der Marke eierlegender Wollmilchsau, nun schon seit geraumer Zeit.

Gestern hat mich mal wieder der Teufel geritten und ich habe meine Rootpartition von Arch kurzerhand von ext4 auf btrfs umstellt.

Als erstes habe ich sichergestellt, dass das Paket btrfs-progs installiert ist.

Danach habe ich den Rechner mit dem Installationsmedium von Arch gebootet.

Mittels "fsck.ext4 -f /dev/sda3" habe ich vorsichtshalber erst mal das vorhandene Dateisystem auf Fehler getestet. Als das keine Probleme ausgespuckt hat, habe ich kurzerhand mittels "btrfs-convert /dev/sda3" meine Rootpartition von ext4 auf btrfs konvertiert. Hier muss man durchaus einige Zeit warten. Nach dem Konvertieren habe ich dann die "neue" Rootpartition gemountet und die /etc/fstab angepasst indem ich beim Eintrag für die betreffende Partition ext4 gegen btrfs und fs_passno von 1 gegen 0 ausgetauscht habe.

Mutig (oder dumm) wie ich bin, habe ich dann gleich einmal einen Neustart hingelegt. Und schwups hat es eine Fehlermeldung gehagelt. Und zwar dass das Filesystem btrfs nicht bekannt sei. Nach einigen ratlosen Minuten habe ich dann wieder das Installationsmedium gebootet, die Partition gemountet und mir die Datei /etc/mkinitcpio.conf angesehen. Hier hatte ich zwar als Hook filesystems eingetragen, aber scheinbar mag das btrfs nicht. Da meines Wissens ein btrfs-Hook existiert habe ich diesen mal schnell hinzugefügt. Damit das ganze dann auch funktioniert, wollte ich dann noch "mkinitcpio -p linux" ausführen. Und wieder hat es peng gemacht. Ohne chroot funktioniert das ja nicht. Also noch schnell die Boot-Partition gemountet und mittels "chroot /mnt/arch" das ganze gechrootet. Nun hat auch "mkinitcpio -p linux" funktioniert. Also Neustart. Und wieder peng. Langsam genervt, habe ich erneut vom Installationsmedium gebootet. Mittels "blkid" habe ich dann mir mal alle Partitionen zu Gemüte geführt und diese mit den Einträgen in der /etc/fstab abgeglichen. Bingo, die UUID hat sich geändert. Also schnell noch diese in der /etc/fstab anpassen. Neustart. Kein Peng, sondern der gewohnte Bootvorgang.

System läuft, Daten sind noch da. Also noch einen Schritt weiter. Erneut habe ich die Datei /etc/fstab editiert und in die betreffende Zeile noch ein compress=lzo hinzugefügt, damit die Dateien, welche geändert werden bzw. neu hinzukommen, auch komprimiert werden. Was aber mit den bereits vorhandenen, die sich nicht ändern? Naja erst mal testen und deshalb... Neustart. Funktioniert. Also was nun mit den bereits vorhandenen Daten? Nach der einen oder anderen Suchabfrage bei Google hatte ich die Lösung. Mit dem Befehl "find -xdev -type f -exec btrfs fi defrag '{}' \;" werden vorhandene btrfs-Filesystem defragmentiert und dabei auch noch komprimiert, sofern der Eintrag in der /etc/fstab vorhanden ist.

Mal sehen, wie sich btrfs nun schlägt. Bisher habe ich noch keine negativen Effekte erlebt. Gut, nach nicht mal 24 Stunden ist das auch kein Wunder. Sollte es wirklich richtig Peng machen, werde ich einfach die ext4-Sicherung einspielen und hier noch einen Artikel schreiben. Alles in allem ist das aber alles kein Hexenwerk. Sofern man die Dinge berücksichtigt, die ich nicht berücksichtigt habe. ;-) **Trotzdem will ich noch einmal ganz deutlich sagen, dass btrfs noch nicht als stabil gekennzeichnet ist. Deswegen Benutzung auf eigene Gefahr.** Genau deswegen bleibt /home bei mir auch erst einmal ext4, da hier wesentlich mehr Daten lagern und eine Datensicherung nicht mal eben eingespielt ist.
