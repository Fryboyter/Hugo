---
title: Dateisystem Btrfs wird demnächst Swap-Dateien unterstützen
date: 2018-12-14T10:46:00+0100
categories:
- Linux
- OSBN
tags:
- Dateisystem
- Btrfs
- Swap
slug: dateisystem-btrfs-wird-demnaechst-swap-dateien-unterstuetzen
---
Seit Jahren verwende ich auf meinen privaten Rechnern kein Swap. Für spezielle Fälle war es aber ganz nützlich mal eben eine Swap-Datei anzulegen. Seit ich Btrfs nutze, war dies leider keine Option mehr, da dieses Dateisytem keine Swap-Dateien unterstützt. Das wird sich demnächst voraussichtlich aber wieder ändern.

Warum wieder? Im Jahre 2009 wurde die Unterstützung von Swap-Dateien [entfernt](https://git.sphere.ly/dtc/kernel_moto_falcon/commit/35054394c4b3cecd52577c2662c84da1f3e73525?w=1), da Swap-Dateien Probleme gemacht haben. Der Entwickler Omar Sandoval hat nun aber kürzlich einen [Patch](https://git.kernel.org/pub/scm/linux/kernel/git/kdave/linux.git/commit/?h=for-next&amp;id=fc2db0ecbdb9f6239688a381fe800cd0cf0a3e4a)eingereicht, der die sichere Nutzung von Swap-Files unter Btrfs ermöglicht. Wenn es keine Probleme damit gibt, könnte diese Änderung bereits in der übernächsten Version des Kernels (voraussichtlich März 2019)\_enthalten sein.
