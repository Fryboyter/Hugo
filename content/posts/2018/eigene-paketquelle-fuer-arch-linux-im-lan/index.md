---
title: Eigene Paketquelle  für Arch Linux im LAN
date: 2018-09-29T18:41:00+0100
categories:
- Linux
- OSBN
tags:
- Arch
- Linux
- Paketquelle
slug: eigene-paketquelle-fuer-arch-linux-im-lan
---
Seit einigen Wochen nutze ich für die Zwischenablage das Tools CopyQ. Als ich heute die über AUR installierten Pakete aktualisiert habe, wurde mir angezeigt. dass CopyQ nun "orphaned" ist. Somit kümmert sich aktuell niemand um die Aktualisierung von CopyQ im AUR.

Wie es der Zufall so will, wurde zwischenzeitlich auch Version 3.6.1 von CopyQ veröffentlicht. Also muss eine Lösung her. Am einfachsten wäre es wohl, die vorhandene PKGBUILD-Datei zu aktualisieren und mir damit Version 3.6.1 lokal zu installieren. Mit folgenden Schritten dauert das keine zwei Minuten.

* Mit "curl -o PKGBUILD https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=copyq" die PKGBUILD-Datei von Version 3.6.0 herunterladen
* In der Datei dann die Version anpassen
* Mit updpkgsums PKGBUILD die Prüfsumme automatisch anpassen
* Mit makepkg -si PKGBUILD -noconfirm kann man dann das Paket erstellen und installieren. 

An dieser Stelle ist es mir aber aufgefallen, dass ich CopyQ ja auf mehreren Rechnern / VM nutze. Gut, ich könnte mittels makepkg PKGBUILD einfach das Paket erstellen und dies auf den betreffenden Rechnern / VM installieren. Ich möchte aber möglichst die Rolle des Turnschuadmins vermeiden. Also wie löse ich das Problem?

Der Raspberry Pi auf dem Pi Hole läuft, langweilt sich im Grunde genommen. Auf diesem könnte ich eigentlich eine eigenen Paketquelle für das LAN erstellen. Nur ist auf dem Raspberry Pi Debian installiert, so dass ich die Arch-Tools wie repo-add nicht direkt nutzen kann. Naja wieso einfach wenn es auch kompliziert geht?

Als erstes habe ich auf dem Raspberry Pi ein Verzeichnis erstellt, dass als Paketquelle dienen soll. Dieses habe ich dann unter Arch mittels sshfs gemountet und mittels "repo-add /gemountetes_Verzeichnis/raspberry.db.tar" eine leere Paketquellendatenbank erzeugt. Mit der PKGBUILD-Datei von Version 3.6.0 und makepkg PKGBUILD habe ich dann unter Arch das Paket erstellt und dies in das gemountete Verzeichnis kopiert. Mittels "repo-add /gemountetes_Verzeichnis/raspberry.db.tar copyq-3.6.0-1-x86.pkg.tar" habe ich dann die Datenbank aktualisiert. Da man angeblich mit sshfs gemountete Verzeichnisse direkt als Paketquellen nutzen kann, habe ich dann einfach folgenden Eintrag in der /etc/pacman.conf unter Arch erstellt.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[raspberry]
SigLevel = Optional
Server = file:///gemountetes_Verzeichnis</code>
</pre>

Der Versuch mittels "pacman -Syy" die Paketquellen zu aktualisieren ist aber immer bei der Paketquelle raspberry gescheitert, da die Datenbank nicht gefunden werden kann. Und das obwohl der Pfad stimmt und die Dateien vorhanden sind. Selbst mit etwas Google-Fu konnte ich das Problem nicht lösen.

Da auf dem Raspberry Pi ja bereits lighthttpd für die grafische Oberfläche für Pi Hole läuft, ist mir die Idee gekommen, dass ich die Pakete über lighthttpd anbiete. Aber scheinbar sieht Pi Hole es nicht vor, dass man über lighthttpd noch weitere Dienste anbietet. Oder ich bin zu blöd dafür.

Da sich der Raspberry Pi wirklich langweilt, kann man ja einfach Apache installieren. Nein besser nginx, da dieser weniger Resourcen verbraucht. Gesagt getan. In der Konfigurationsdatei /etc/nginx/sites-available/default habe ich dann bei den beiden Zeilen die mit listen beginnen den Port geändert, da ja bereits lighthttpd auf Port 80 läuft. Die Zeile die mit root beginnt, habe ich dann so geändert, dass hier auf das Verzeichnis verwiesen wird, das als Paketquelle dienen soll. Noch etwas weiter unten habe ich den Block location / um die zwei Zeilen allow 192.168.1.1/24; und deny all; erweitert. Somit kann nur noch jemand aus meinem LAN auf nginx zugreifen. Sicher ist sicher. Mit einem Neustart von nginx sorge ich dafür, dass die Änderungen berücksichtigt werden.

Zurück auf dem Rechner mit Arch, auf dem ich die Paketquelle raspberry eingetragen habe, habe ich hier die dritte Zeile auf Server = IP_DES_RASPBERRY:PORT_VON_NGINX geändert. Mit "pacman -Syy" habe ich dann versucht die Paketquellen zu aktualisieren. Was scheinbar auch funktioniert hat, da ich keine Fehlermeldung erhalten habe. Da CopyQ über AUR installiert wurde, habe ich nun CopyQ deinstalliert und mittels pacman und der Paketquelle raspberry wieder installiert. Auch das hat funktioniert.

Da ich ja Version 3.6.1 installieren möchte, habe ich dann wie oben beschrieben die PKBUILD-Datei angepasst und das aktuelle Paket erzeugt. Dies habe ich dann wieder in das gemountete Verzeichnis gepackt und mit "repo-add /gemountetes_Verzeichnis/raspberry.db.tar copyq-3.6.1-1-x86.pkg.tar" die Datenbank aktualisiert. Als ich dann mittels "pacman -Syu" auf Updates geprüft haben, wurde mir Version 3.6.1 von CopyQ angeboten, welche ich gleich installiert habe.

Abschließend habe ich dann noch bei allen betreffenden Rechnern CopyQ deinstalliert, die neue Paketquelle hinterlegt und aktualisiert und CopyQ über diese neu installiert.

Vermutlich wäre es einfacher gewesen, einfach die Betreuuung von CopyQ im AUR zu übernehmen. Aber das hätte weniger Spaß gemacht. Und wie schon weiter oben angegeben. Warum einfach, wenn es auch kompliziert geht? Zudem kann ich in meiner Paketquelle so viel Mist bauen wie ich willl ohne dafür einen verbalen Einlauf von Dritten zu erhalten. Und ich werde die Paketquelle wohl auch in mein Ansible-Projekt einbauen. Und da ich einige AUR-Pakete installiert habe, deren Betreuer sich oft ziemlich viel Zeit mit dem Aktualisieren lassen, wird es auch nicht bei einem Paket bleiben.
