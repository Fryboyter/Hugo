---
title: Windows leichter mit Syslinux starten
date: 2019-09-22T11:15:12+0200
categories:
- OSBN
- Linux
tags:
- Syslinux
- Chainloading
- Windows
slug: windows-leichter-mit-syslinux-starten
---
Wenn man mit dem Bootloader [syslinux](https://www.syslinux.org/) neben Linux auch Windows starten will, erfolgt dies bei Festplatten mit MBR (nicht GPT!) beispielsweise über folgenden Eintrag in der Datei /boot/syslinux/syslinux.cfg.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">...
LABEL windows
	MENU LABEL Windows
	COM32 chain.c32
	APPEND hd0 3
...
</code>
</pre>

Hd0 ist in diesem Fall die erste vom BIOS/UEFI erkannte Festplatte. Und 3 bezieht sich auf die dritte Partition auf dieser Festplatte. Was aber wenn man mehrere Festplatten installiert hat und Windows nicht auf der gleichen Platte wie Linux installiert ist? Man müsste herausfinden in welcher Reihenfolge das BIOS/UEFI die Festplatten erkennt. Hierbei muss man beachten, dass Festplatten ab 0 gezählt werden, Partitionen aber ab 1. Also warum das ganze nicht etwas einfacher lösen?

Mit dem Befehl "fdisk -l" lässt man sich zuerst die ganzen vorhandenen Festplatten anzeigen und sucht sich dann die Festplatte, auf der Windows installiert ist, heraus. Sollte man wissen auf welcher Festplatte Windows installiert ist, kann man sich diese auch direkt mit beispielsweise "fdisk -l /dev/sde" anzeigen lassen. Das sieht dann beispielsweise wie folgt aus.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">Festplatte /dev/sde: 238,49 GiB, 256060514304 Bytes, 500118192 Sektoren
Festplattenmodell: Crucial_CT256MX1
Einheiten: Sektoren von 1 * 512 = 512 Bytes
Sektorgröße (logisch/physikalisch): 512 Bytes / 4096 Bytes
E/A-Größe (minimal/optimal): 4096 Bytes / 4096 Bytes
Festplattenbezeichnungstyp: dos
Festplattenbezeichner: 0x0000d958

Gerät      Boot    Anfang      Ende  Sektoren  Größe Kn Typ
/dev/sde1  *         2048    206847    204800   100M  7 HPFS/NTFS/exFAT
/dev/sde2          206848 499123111 498916264 237,9G  7 HPFS/NTFS/exFAT
/dev/sde3       499124224 500113407    989184   483M 27 Verst. NTFS WinRE
</code>
</pre>

Wichtig ist hier im Grunde nur der Festplattenbezeichner. Diesen merken wir uns und ändern den Eintrag von Windows in der Konfigurationsdatei von syslinux wie folgt ab.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">...
LABEL windows
	MENU LABEL Windows
	COM32 chain.c32
	APPEND mbr:0x0000d958
...
</code>
</pre>

Mit diesem Eintrag sollte man Windows nun problemlose per Chainloading starten können.