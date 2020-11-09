---
title: "EXT4-fs (mmcblk0p2): couldn''t mount as ext3 due to feature incompatibilities"
date: 2015-05-03T11:12:00+0100
categories:
- Linux
- OSBN
tags:
- Raspberry Pi
- Mount
- Ext2
- Ext3
- Ext4
slug: ext4-fs-mmcblk0p2-couldnt-mount-as-ext3-due-to-feature-incompatibilities
---
In der Logdatei meines Raspberry Pi tauchen nach jedem Start die Fehlermeldungen "EXT4-fs (mmcblk0p2): couldn't mount as ext3 due to feature incompatibilitie" und "EXT4-fs (mmcblk0p2): couldn't mount as ext2 due to feature incompatibilities" auf. Es funktioniert zwar alles aber es nervt. Vor allem weil mmcblk0p2 in dem Fall ext4 und nicht ext3 oder ext2 nutzt. Aber die Lösung ist recht einfach.

Einfach die Datei /boot/cmdline.txt öffnen und rootfstype=ext4 hinzufügen und abspeichern. Nach einem Neustart ist die Fehlermeldung verschwunden. Nebenwirkungen konnte ich auch noch keine feststellen.
