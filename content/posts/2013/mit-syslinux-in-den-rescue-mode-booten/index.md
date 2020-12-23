---
title: Mit syslinux in den rescue mode booten
date: 2013-08-25T01:12:00+0100
categories:
- Linux
- OSBN
tags:
- Syslinux
- Rescue
- Booten
slug: mit-syslinux-in-den-rescue-mode-booten
---
Viele Nutzer von Arch Linux verwenden als Bootloader nicht Grub(2) oder LiLo sondern syslinux. Auch ich gehöre zu diesen Nutzern. Standardmäßig gibt es zwei Einträge das System zu booten. Einmal den normalen Aufruf und einmal den Fallback-Modus bei dem alle [mkinitcpio hooks](https://wiki.archlinux.org/index.php/Mkinitcpio#HOOKS "mkinitcpio hooks") geladen werden. Mit beiden Einträgen konnte ich bei meinem [Broadcom-Problem](/warum-man-immer-erst-die-sufu-nutzen-sollte/ "Warum man immer erst die SuFu nutzen sollte") das bei einem Kernel, aktueller Version 3.10.5, auftritt, nichts anfangen. Um bei einem ähnlichen Problem zukünftig gewappnet zu sein, habe ich mir jetzt eine Lösung zusammen gebastelt, so dass ich in vielen Fällen auf ein Booten mit dem Installationsmedium und anschließendem chroot verzichten kann.

Hierzu habe ich einfach mit dem Befehl **nano /boot/syslinux/syslinux.cfg** die Konfigurationsdatei des Bootloaders geöffnet. Der, für mein Vorhaben wichtige Teil sieht wie folgt aus.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">LABEL arch
MENU LABEL Arch Linux
LINUX ../vmlinuz-linux
APPEND cryptdevice=/dev/sda2:main root=/dev/mapper/main-root ro lang=de locale=de_DE.UTF-8
INITRD ../initramfs-linux.img

LABEL archfallback
MENU LABEL Arch Linux Fallback
LINUX ../vmlinuz-linux
APPEND cryptdevice=/dev/sda2:main root=/dev/mapper/main-root ro lang=de locale=de_DE.UTF-8
INITRD ../initramfs-linux-fallback.img</code>
</pre>

Hier haben wir als erstes den normalen Start und als zweites den Fallback-Modus.

Jetzt möchte ich noch einen dritten Eintrag haben, der mir erlaubt in etwas ähnliches wie den früheren Runlevel 1 zu booten, den es in der Form ja unter systemd nicht mehr gibt.

Von daher kopiere ich erst einmal den ersten Block unter den zweiten und erzeuge somit einen dritten Eintrag im Bootmenü. Nun passe ich die Zeile LABEL und MENU LABEL entsprechend an, damit diese einzigartig sind und man erkennen kann, was die Funktion dahinter ist.

Zu guter Letzt ändere ich noch die Zeile APPEND und erweitere sie am Ende um systemd.unit=rescue und speichern die Datei einfach ab. Mehr ist nicht nötig. Das Ganze müsste dann folgendermaßen aussehen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">LABEL archrescue
MENU LABEL Arch Rescue
LINUX ../vmlinuz-linux
APPEND cryptdevice=/dev/sda2:main root=/dev/mapper/main-root ro lang=de locale=de_DE.UTF-8 systemd.unit=rescue
INITRD ../initramfs-linux.img</code>
</pre>

Durch systemd.unit=rescue wird das System angewiesen in den Modus zu booten, der dem ehemaligen Runlevel 1 am nächsten kommt. Sprich es ist alles gemountet was nötig ist, aber sonst läuft so gut wie nichts. Zum Beispiel kein Netzwerk, was ja bei mir die Kernel Panic ausgelöst hat. Um bei dem Broadcom-Problem zu bleiben könnte man hier zum Beispiel mit dem Befehl **pacman -U /var/cache/pacman/pkg/linux-3.10.5-1-x86_64.pkg.tar.xz** den Kernel downgraden und somit das System wieder lauffähig machen, bis das Problem behoben ist. Dies wird in diesem Fall wohl frühestens in Version 3.11 soweit sein.
