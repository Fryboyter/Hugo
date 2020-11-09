---
title: Achtung beim Klonen einer Btrfs-Partition
date: 2014-12-26T16:07:00+0100
categories:
- Linux
- OSBN
tags:
- Partition
- Klonen
- Btrfs
- Dateisystem
slug: achtung-beim-klonen-einer-btrfs-partition
---
Da ich zu Weihnachten eine SSD bekommen habe, habe ich die Partitionen meiner Linux-HDD kurzerhand auf die SSD geklont. Da ich solchen Vorgängen nicht 100%ig vertraue wollte ich die normale Festplatte erst einmal ohne Änderungen im System belassen. Quasi als Backup. Nachdem ich im UEFI die Bootreihenfolge umgestellt hatte, konnte ich auch wunderbar von der SSD booten. Allerdings war das Ganze nicht schneller als per HDD und eine der HDD hatte dabei auch Schreib- bzw. Lesezugriffe.

Hmmm... der Groschen ist recht schnell gefallen. Ich mounte über die UUID der Partitionen. So kann ich eine SATA-Platte abklemmen und auf einen anderen SATA-Port anschließen und der Rechner bootet weiterhin, da sich die UUID nicht ändert. Auch beim Klonen nicht. Somit hatte ich auf der SSD als auch der HDD die gleichen UUID und die wurden beide gnadenlos gemountet. Zweimal /, zweimal /boot und zweimal /home. Das es dabei nichts zerrissen hat, war vermutlich Glück. Beim letzten Festplatten-Umzug habe ich mittels tune2fs /dev/sdXY -U urandom einfach neue UUID vergeben (anstelle von sdXY sollte man natürlich die Partitionen der alten Platte angeben). Wie schon angemerkt habe ich eigentlich drei Partitionen. Einmal /boot, einmal / und einmal /home. Boot habe ich, da dort nichts wichtiges liegt, kurzerhand von der alten Platte getilgt. Home (ext4) konnte ich mit genanntem Befehl eine neue UUID verpassen. Nur / hat sich standhaft geweigert. Dort setze ich Btrfs als Dateisystem ein. Tune2fs ist aber nur für ext2 bis ext4. Aber es gibt ja btrfstune. Hier gibt es allerdings keine Möglichkeit die UUID zu ändern. Herzlichen Glückwunsch, das ist bei Btrfs auch nicht vorgesehen.

Wer also auf die Idee kommt, eine Btrfs-Partition zu klonen und beide Partition hinterher mounten zu wollen, sollte hier lieber dann bei einer der beiden Partitionen auf /dev/sdXY oder das Label der Partition zurückgreifen und nicht auf die UUID. Nur so als kleiner Hinweis am Rande.
