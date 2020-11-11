---
title: PKGBUILD für Bogofilter 1.2.3
date: 2013-02-08T17:20:00+0100
categories:
- Linux
- OSBN
tags:
- Bogofilter
- PKGBUILD
slug: pkgbuild-fuer-bogofilter-1-2-3
---
Ich habe mir mal wieder eine PKGBUILD-Datei für Arch zusammengebaut. Dieses mal musste Bogofilter (ein E-Mail-Spamfilter den ich nutze) herhalten. Das Paket wurde vor einigen Tagen als veraltet markiert, die derzeit aktuelle Version, die ein Sicherheitsproblem behebt, gibt es allerdings (leider) schon wesentlich länger. Da ich nicht warten will, bis der Betreuer des Paketes in die Gänge kommt, hier mal die Datei. Eventuell kann es ja jemand gebrauchen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash"># $Id$
# Maintainer: tobias
# Contributor: Low Kian Seong
pkgname=bogofilter
pkgver=1.2.3
pkgrel=1
pkgdesc="A fast Bayesian spam filtering tool"
arch=('i686' 'x86_64')
license=('GPL3')
url="http://bogofilter.sourceforge.net"
depends=('db' 'perl' 'gsl')
backup=('etc/bogofilter/bogofilter.cf')
source=(http://sourceforge.net/projects/${pkgname}/files/${pkgname}-current/${pkgname}-${pkgver}/${pkgname}-${pkgver}.tar.bz2)
md5sums=('c3ed7f483b83abcbf6d8c797084bd06e')
build() {
cd "${srcdir}/${pkgname}-${pkgver}"
./configure --prefix=/usr \
                  --sysconfdir=/etc/bogofilter \
                  --localstatedir=/var \
                  --enable-transactions
make
}

package() {
cd "${srcdir}/${pkgname}-${pkgver}"
make DESTDIR="${pkgdir}" install@speedymail.org>@archlinux.org>

mv "${pkgdir}/etc/bogofilter/bogofilter.cf.example" "${pkgdir}/etc/bogofilter/bogofilter.cf"

install -dm755 "${pkgdir}/usr/share/${pkgname}/contrib"
install -m644 contrib/* "${pkgdir}/usr/share/${pkgname}/contrib/"
}
</code>
</pre>

Geändert wurde auch hier nur die Zeilen pkgver und md5sums. Das ganze gibt es natürlich auch wieder unter [https://spideroak.com/browse/share/datengrab/FryBoyter](https://spideroak.com/browse/share/datengrab/FryBoyter "https://spideroak.com/browse/share/datengrab/FryBoyter"). Benutzung wie immer ohne Gewähr.
