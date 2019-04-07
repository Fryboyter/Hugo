---
title: Externe Speichermedien mit udisks2 unter /media/ mounten
date: 2016-01-24T15:38:00+0100
categories:
- Linux
- OSBN
tags:
- Udisks2
- Mounten
slug: externe-speichermedien-mit-udisks2-unter-media-mounten
---
Nutzt man udisks2 zum Mounten von z. B. externen Festplatten wird hierfür unter /run/media/Benutzername/ ein Mountpoint erstellt, der entweder der UUID oder dem Label des Mediums entspricht. In diesem Verzeichnis greift ACL, was auf einem System mit mehreren Benutzern durchaus Sinn machen kann. Auf meinen Rechnern bin ich aber der alleinige Nutzer und mit geht das Mounten unter /run/media/Benutzername/xyz/ auch ehrlich gesagt einfach auf den Zeiger.

Wie also bekommt man udisks2 dazu unter /media/xyz/ zu mounten? Erst einmal erstellt unter /etc/udev/rules.d/ einfach die Datei 99-udisks2.rules. In diese schreibt man dann noch ENV{ID_FS_USAGE}=="filesystem|other|crypto", ENV{UDISKS_FILESYSTEM_SHARED}="1". Die 1 bedeutet, dass der Mountpoint unter /media/ erstellt wird. Ändert man das ganze auf 0 wird wieder /run/media/Benutzername/ verwendet. Sollte das Verzeichnis /media/ noch nicht vorhanden sein, sollte man es abschließend noch als Root erstellen. Ansonsten funktioniert es nicht wirklich.
