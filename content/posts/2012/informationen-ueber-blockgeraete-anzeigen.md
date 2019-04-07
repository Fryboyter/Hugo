---
title: Informationen über Blockgeräte anzeigen
date: 2012-12-13T21:47:00+0100
categories:
 - Linux
 - OSBN
tags:
- Informationen
- Blockgeräte
- Lsblk
slug: informationen-ueber-blockgeraete-anzeigen
---
<p>Heute bin ich mal wieder über ein Tool gestolpert, dass ich kurz vorstellen will. Es handelt sich hierbei um lsblk.

Führt man den Befehl ohne Parameter aus, erhält man beispielsweise folgende Ausgabe.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[root@netbook ~]# lsblk 
NAME                   MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                      8:0    0 298,1G  0 disk  
├─sda1                   8:1    0  94,1M  0 part  /boot
└─sda2                   8:2    0   298G  0 part  
  └─main (dm-0)        254:0    0   298G  0 crypt 
    ├─main-root (dm-1) 254:1    0    30G  0 lvm   /
    ├─main-swap (dm-2) 254:2    0    16G  0 lvm   [SWAP]
    └─main-home (dm-3) 254:3    0   252G  0 lvm   /home</code>
</pre>

Das ganze lässt sich über diverse Parameter noch ziemlich erweitern bzw. eingrenzen. Mit dem Parameter -f kann man sich beispielsweise noch die UUID anzeigen lassen. Mehr erfährt man in der Manpage.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[root@netbook ~]# lsblk -f
NAME                   FSTYPE      LABEL UUID                                   MOUNTPOINT
sda                                                                             
├─sda1                 ext4        boot  f2859c78-5073-4134-8792-337d944ca37e   /boot
└─sda2                 crypto_LUKS       a8751c65-3549-4f75-8d42-399915c93ccf   
  └─main (dm-0)        LVM2_member       fNkm7V-hkpi-4sP7-H54e-5qod-GelW-zRwEz7 
    ├─main-root (dm-1) ext4        root  61ce4471-67bc-4a18-9c80-0a75c075e899   /
    ├─main-swap (dm-2) swap        swap  3cbfb365-e6c6-4bd1-8459-d04ed7c7858e   [SWAP]
    └─main-home (dm-3) ext4        home  1c4bf4c8-8e2c-444a-8121-beb54e48202a   /home</code>
</pre>

Lsblk gibt die Informationen übrigens auch aus, wenn die Partitionstabelle nicht gültig ist.
