---
title: Btrfs-Treiber für Windows
date: 2016-02-23T09:09:00+0100
categories:
- Linux
- OSBN
tags:
- Btrfs
- Treiber
- Windows
slug: btrfs-treiber-fuer-windows
---
Um unter Windows auf Partitionen mit dem Dateisystem ext3/4 zugreifen zu können gibt es Tools wie den [Linux Reader](http://www.diskinternals.com/linux-reader) von Diskinternal. Für Partitionen mit dem Dateisystem Btrfs ist mir noch kein funktionierendes Programm untergekommen. Wenn man also, wie ich, Btrfs nutzt und unter Windows mal eben auf die Linux-Partitionen zugreifen will ist das blöd. Die Situation könnte sich nun eventuell ändern.

Der Nutzer maharmstone hat auf Github eine erste Version von [WinBtrfs](https://github.com/maharmstone/btrfs) veröffentlicht. Laut dem Entwickler ist ein Lese- und Schreibzugriff bereits möglich. Sachen wie RAID oder LZO-Komprimierung werden allerdings derzeit noch nicht unterstützt. Das ganze ist als erste Alpha-Version gekennzeichnet. Von einem produktiven Einsatz sollte man derzeit somit noch absehen. Feedback ist laut maharmstone willkommen. Egal ob positiv oder negativ.
