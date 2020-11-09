---
title: Prüfen ob externes Gehäuse das USB Attached SCSI Protocol beherrscht
date: 2016-09-12T19:24:00+0100
categories:
- Linux
- OSBN
tags:
- USB
- Gehäuse
- UASP
slug: pruefen-ob-externes-gehaeuse-das-usb-attached-scsi-protocol-beherrscht
---
Vor ein paar Tagen hat sich der USB-Anschluss meines externen Fesplattengehäuses von der Platine gelöst (ja ich war da nicht ganz unschuldig...). Als Ersatz habe ich mir das Gehäuse Quickstore Portable von Sharkoon gekauft. Laut den technischen Daten soll es UASP unterstützen.

Bei [UASP](https://en.wikipedia.org/wiki/USB_Attached_SCSI) handelt es sich um ein Protokoll das die Datenübertragung per USB bis zu 30 Prozent beschleunigt. Unter Linux wird das Protokoll ab Kernel 2.7 unterstützt. Aber sicher ist sicher. Daher habe ich vorsichtshalber mal nachgesehen.

Als erstes habe ich mir mittels lsmod | grep usbcore erst einmal die geladenen Module angesehen. Hier wird bei mir unter anderem uas angezeigt. Schon mal nicht schlecht.

Als nächstes habe ich lsusb ausgeführt um mir die USB-Geräte anzuzeigen. Hier habe ich unter anderem folgende Ausgabe erhalten.

>Bus 001 Device 004: ID 357d:7788 Sharkoon QuickPort XT

Hier merkt man sich die Bus- und die Device-Nummer. Abschließen habe ich noch lsusb -t ausgeführt und bei der Ausgabe nach der Zeile gesucht die mit der obigen Bus- und Device-Nummer übereinstimmt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ehci-pci/3p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/6p, 480M
        |__ Port 2: Dev 4, If 0, Class=Mass Storage, Driver=uas, 480M</code>
</pre>

Als Treiber wird hier uas genutzt. Das USB Attached SCSI Protokoll wird also verwendet. Gefühlt ist das neue Gehäuse deutlich schneller, obwohl nur eine ganz normale 2,5 HDD zum Einsatz kommt. Ob das allerdings wirklich nur an UASP liegt, kann ich nicht sagen. Das vorherige Gehäuse war eher von der Marke "Grabbeltisch".
