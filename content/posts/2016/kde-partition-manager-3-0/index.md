---
title: KDE Partition Manager 3.0
date: 2016-12-19T12:21:00+0100
categories:
- Linux
- OSBN
tags:
- Plasma
- Partitionen
- Verwalten
slug: kde-partition-manager-3-0
---
Wenn möglich nutze ich unter Linux KDE Plasma. Der dort enthaltene Partition Manager zum Ändern der Partitionen hatte bisher immer Probleme mit LUKS in Verbindung mit LVM (oder umgekehrt).

Gestern wurde nun Version 3.0 des KDE Partition Managers veröffentlicht. Über das Changelog habe ich mich in dem Fall mal wirklich gefreut, da ich viel mit LVM / LUKS arbeite und bisher immer auf alternative grafische Oberflächen ausgewichen bin oder die die Befehle per Hand eingegeben habe.

- Both LVM on LUKS and LUKS on LVM configurations are now supported.
- Creating new LVM Volume Groups, adding or removing LVM Physical Volumes from LVM VG.
- Resizing LVM Logical Volumes.
- Resizing LVM Physical Volumes even if they belong to LVM Volume Group (used extents will be moved out somewhere else)
- Added support for online resize. Not all filesystems support this, e.g. ext4 can only be grown online while btrfs supports both growing and shrinking.
- Fixed some crashes, Qt 5.7.1 is also recommended to fix crash (in Qt) on exit.
- Better support for sudo. Now KDE Partition Manager declares required environmental variables when kdesu uses sudo (e.g. in Kubuntu or Neon), so the theming is no longer broken. Also environmental variables for Wayland are also fixed.

{{< youtube FKCQ7pJN1vY >}}
