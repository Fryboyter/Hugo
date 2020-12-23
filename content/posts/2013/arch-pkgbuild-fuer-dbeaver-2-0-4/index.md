---
title: Arch PKGBUILD für Dbeaver 2.0.4
date: 2013-01-05T16:38:00+0100
categories:
- Linux
- OSBN
tags:
- DBeaver
- PKGBUILD
slug: arch-pkgbuild-fuer-dbeaver-2-0-4
---
Wie schon [hier](/alternative-zu-mysql-workbench/ "Alternative zu MySQL-Workbench") geschrieben, bin ich von Dbeaver recht angetan. Inzwischen nutze ich es eigentlich ausschließlich und auch einige meiner Kollegen konnte ich anfixen. Die aktuelle Version 2.0.4 steht unter Arch im AUR allerdings derzeit nicht zur Verfügung. Eventuell ist der Betreuer des Paketes ja noch im Urlaub. Da ich allerdings bei manchen Paketen etwas ungeduldig bin, habe ich mir das Ganze mal zur Brust genommen und die Datei PkGBUILD angepasst. Herausgekommen ist folgendes:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash"># Maintainer: Arne Hoch
pkgname=dbeaver
pkgver=2.0.4
pkgrel=1
pkgdesc=&quot;a free universal database tool for developers and database administrators&quot;
arch=(&#039;i686&#039; &#039;x86_64&#039;)
url=&quot;http://dbeaver.jkiss.org/&quot;
license=(&quot;Freeware&quot;)
depends=(&#039;java-runtime&gt;=1.6&#039; &#039;gtk2&#039;)
makedepends=(&#039;unzip&#039;)
if [ &quot;$CARCH&quot; = &quot;i686&quot; ];
then source=(http://dbeaver.jkiss.org/files/dbeaver-$pkgver-linux.gtk.x86.zip dbeaver.desktop) md5sums=(&#039;298d4ced68e90dce75f896802c01b0a0&#039;)
else
source=(http://dbeaver.jkiss.org/files/dbeaver-$pkgver-linux.gtk.x86_64.zip dbeaver.desktop) md5sums=(&#039;02ba30d3e38e2700081d5bd88d47aed5&#039;)
fi
md5sums+=(&#039;6944e8324464e5802ddf6292026593d6&#039;)

build() {
mkdir -p $pkgdir/opt/
mkdir -p $pkgdir/usr/share/applications
mkdir -p $pkgdir/usr/bin
cd $srcdir
cp -r $pkgname $pkgdir/opt/
ln -s /opt/dbeaver/dbeaver $pkgdir/usr/bin/
install -m 644 $srcdir/dbeaver.desktop $pkgdir/usr/share/applications/
}
</code>
</pre>

Die Installation funktioniert und das Programm an sich auch. Soviel kann ich also nicht versaut haben. Naja im Grunde genommen habe ich ja nur die MD5-Summen sowie die pkgver-Zeile angepasst. Die letzte Zeile bei dem MD5-Summen (die mit dem +) ist übrigens für die Datei dbeaver.desktop über die ein Eintrag im Startmenü erzeugt wird. Wer sich keine Arbeit machen will, findet die Dateien unter [https://spideroak.com/browse/share/datengrab/FryBoyter](https://spideroak.com/browse/share/datengrab/FryBoyter). Nutzung, wie immer, auf eigene Gefahr und ohne Gewähr (und Gewehr).
