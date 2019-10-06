---
title: Arch Linux schneller starten
date: 2012-06-16T11:12:00+0100
categories:
- Linux
- OSBN
tags:
- Arch Linux
- Systemd-analyze
slug: arch-linux-schneller-starten
---
Eigentlich ist es mir egal, wie schnell die bei mir installierten Betriebssysteme starten. Zumindest wenn es nicht mehrere Minuten dauert. Aber gestern ist bei mir mal wieder der Spieltrieb ausgebrochen. Darum habe ich mir mal den Bootvorgang von Arch Linux vorgenommen. Als erstes habe ich mir mal angesehen wie schnell das System derzeit startet. Da ich systemd einsetze habe ich das mit dem Befehl **systemd-analyze** gemacht. Hier wird angezeigt, welche Services usw. wie lange gebraucht haben. Sortiert wird das ganze von lange bis kurz. Insgesamt hat das System gut 30 Sekunden gebraucht (da ich die alten Werte nicht gespeichert habe, bitte folgende zwei Beispiele nur als Beispiele ansehen).

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">systemd-analyze Startup finished in 11278ms (kernel) + 19325ms (userspace) = 30603ms</code>
</pre>

Im Grunde also ein Wert, bei dem zumindest ich nicht meckern kann. Dank meines Spieltriebs wollte ich aber trotzdem mal sehen, was möglich ist. Als nächstes haben ich mir mittels **systemd-analyze blame** anzeigen lassen, was wie lange zum starten gebraucht hat.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">systemd-analyze blame
2802ms systemd-readahead-collect.service
2756ms systemd-readahead-collect.service systemd-readahead-replay.service
2727ms systemd-logind.service
2669ms media-WindowsD.mount
2668ms media-WindowsC.mount
2664ms console-kit-daemon.service
2620ms network.service
2600ms dbus.service
1465ms systemd-remount-fs.service
1273ms systemd-udev-trigger.service
1094ms dev-mqueue.mount
1090ms sys-kernel-debug.mount
890ms systemd-user-sessions.service
850ms systemd-sysctl.service
827ms dev-hugepages.mount
609ms systemd-vconsole-setup.service
460ms console-kit-log-system-start.service
451ms systemd-modules-load.service
308ms systemd-tmpfiles-setup.service
306ms media-WindowsD.mount
239ms systemd-udev.service
156ms openvpn@NL4.service
123ms home.mount
43ms tmp.mount
39ms upower.service
16ms udisks2.service
5ms boot.mount
1ms rtkit-daemon.service
1ms sys-fs-fuse-connections.mount</code>
</pre>

Da ich [e4rat](https://wiki.archlinux.org/index.php/E4rat "e4rat") verwende habe ich mittels **systemctl disable systemd-readahead-collect.service systemd-readahead-replay.service** die beiden vergleichbaren systemd-Services deaktiviert, da diese recht lange gebraucht haben. Viel mehr konnte ich nicht deaktivieren, da ich leider alle andere was langsam gestartet wurde, brauche. In der mittels systemd-analyze blame erzeugten List ist mir allerdings noch aufgefallen, dass es relativ lange dauert, bis zwei NTFS-Partitionen gemountet werden. Da ich diese nicht sofort nach dem Start und auch nicht regelmäßige brauche, habe ich mir mal die /etc/fstab vorgenommen. Systemd bietet hier die Möglichkeit, bestimmte Partitionen erst zu mounten, wenn man auf die Mountpoints zugreift. Das sollte wieder etwas bringen. Also habe ich einen Blick in die fstab geworfen. Eine der betreffenden Einträge sah z. B. so aus.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">UUID=DE084E95084E6C99 /media/WindowsC ntfs-3g default 0 0</code>
</pre>

Hier muss nun das default gegen noauto,comment=systemd.automount ausgetauscht werden, so dass wir folgenden Eintrag erhalten.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">UUID=DE084E95084E6C99 /media/WindowsC ntfs-3g noauto,comment=systemd.automount 0 0</code>
</pre>

So wird in diesem Fall die Partition die über /media/WindowC angesprochen wird, erst dann gemountet, wenn man auf den Mountpoint zugreift. Und schon hat das System wieder etwas schneller gebootet. Wirklich schneller wurde der Spaß aber erst, als ich auch noch den Eintrag für /home angepasst habe. Das hat richtig etwas bewirkt. Als letztes habe ich dann noch die unnötigen Terminals, wie [hier](https://wiki.archlinux.org/index.php/Improve_Boot_Performance#TTY_terminal_management)beschrieben deaktiviert. Und was hat mir das ganze jetzt gebracht? Etwas Spass an der Freude und ein System, dass nun in ca. 18 Sekunden anstelle von 30 bootet. Ich vermute allerdings, dass man den Bootvorgang noch weiter optimieren könnte. Aber dafür müsste man, wenn man den diversen Anleitungen vertraut, zu sehr ins System eingreifen. Das lasse ich mal lieber.
