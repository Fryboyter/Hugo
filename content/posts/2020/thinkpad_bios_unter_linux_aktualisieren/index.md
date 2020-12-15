---
title: BIOS eines Thinkpads aktualisieren
date: 2020-02-19T21:58:40+0100
categories:
- OSBN
- Linux
tags:
- Thinkpad  
- BIOS
- Lenovo
slug: thinkpad-bios-eines-thinkpads-aktualisieren
---
Ich habe hier ein Thinkpad vor mir liegen bei dem aufgrund einer Sicherheitslücke ein Update des BIOS / UEFI nötig ist. Lenovo bietet zwar eine entsprechende Iso-Datei zum Download an aber diese lässt sich unter Linux nicht einfach so auf einen USB-Stick kopieren. Die Lösung ist allerdings recht einfach.

Als erstes besorgt man sich bei Lenovo die Iso-Datei der Boot-CD für sein Thinkpad. Nehmen wir beispielsweise die, die man [hier](https://pcsupport.lenovo.com/us/de/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x230/downloads/ds029187) herunterladen kann.

Als nächstes installiert man sich das Script geteltorito.pl. Bei Arch findet man es im AUR. Alternativ findet man es [hier](https://userpages.uni-koblenz.de/~krienke/ftp/noarch/geteltorito/geteltorito/geteltorito.pl).

Mit diesem extrahiert man mit folgendem Befehl das El-Torito-Boot-Image aus der Iso-Datei.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">geteltorito.pl -o bios.img g2uj33us.iso
</code>
</pre>

Die Bezeichnung der Iso-Datei muss man ggf. anpassen.

Abschließend schreibt man mit folgendem Befehl die Img-Datei auf den USB-Stick.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">dd bs=64K if=/pfad/zu/bios.img of=/dev/sdX status=progress oflag=sync
</code>
</pre>

Den Teil mit if= und of= muss man an die eigenen Gegebenheiten anpassen. Alternativ kann man auch Tools wie [Etcher](https://www.balena.io/etcher/) nutzen.

Nun sollte man von dem USB-Stick booten und das BIOS / UEFI aktualisieren können.
