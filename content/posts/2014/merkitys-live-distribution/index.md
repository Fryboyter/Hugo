---
title: Merkitys - Live-Distribution
date: 2014-12-03T18:50:00+0100
categories:
- Linux
- OSBN
tags:
- Merkitys
- Live Distribution
- Linux
slug: merkitys-live-distribution
---
Urlaubszeit ist Bastelzeit. Und da ich gerade Urlaub habe bastle ich mir gerade meine eigene Live-Distribution zusammen. Als Basis nehme ich Arch Linux. Hier mal eine Zusammenfassung, was ich bisher gemacht habe.

**Der komplette Vorgang erfolgt, wie im Arch-Wiki angegeben, komplett mit Root-Rechten.**

Um sich eine eigene Live-Distribution zu erstellen benötigt man das Paket archiso. Dieses habe ich mir mittels pacman -S archiso kurzerhand installiert. Als nächstes habe ich mir ein Arbeitsverzeichnis erstellt (mkdir /home/benutzer/archlive). Hierbei ist zu beachten, dass der ganze Spass einiges an Speicher benötigt. Daher habe ich das Verzeichnis auch kurzerhand im Homeverzeichnis meines normalen Benutzerkontos erstellt. Beim ersten Versuch hatte ich das Verzeichnis im Verzeichnis von root erstellt und mir beim Anlegen des Isos die komplette Partition geflutet was das Betriebssystem gar nicht lustig fand...

Nun habe ich mittels cp -r /usr/share/archiso/configs/PROFILE/ /home/benutzer/archlive alle Dateien und Verzeichnisse in das eben angelegte Arbeitsverzeichnis kopiert. Jetzt kann der Spass beginnen.

Im Unterverzeichnis releng im Arbeitsverzeichnis findet man eine Datei namens build.sh. Mit dieser wird die Iso-Datei erstellt. Für meine Bedürfnisse waren allerdings Änderungen nötig. Folgende Dinge habe ich daher kurzerhand geändert.

- Bei iso_name= habe ich archlinux gegen Merkitys ausgetauscht. Somit wird schlussendlich die Datei Merkitys-$Datum.iso erzeugt. Anstelle von $Datum wird das jeweils aktuelle Datum angezeigt an dem die Datei erstellt wurde. Also z. B. Merkitys-2014-12-03.iso

- Ein ganzes Stück weiter unten gibt es die Zeile "mkarchiso ${verbose} -w "${work_dir}" -D "${install_dir}" -L "${iso_label}" -o "${out_dir}" iso "${iso_name}-${iso_version}-dual.iso"". Hier habe ich das -dual entfernt, da ich eine reine 64Bit-Version haben möchte.

- Fast ganz am Ende der Datei finden sich drei Zeilen mit folgendem Inhalt: "for arch in i686 x86_64; do". Damit auch wirklich nur die 64-Bit-Version erstellt wird habe ich kurzerhand einfach das i686 entfernt und die Datei abgespeichert.

Im gleichen Verzeichnis findet man die Dateien packages.x86_64, packages.i686 und packages.both. In der ersten Datei werden die Pakete eingetragen die für 64 Bit gelten. In der zweiten die für 32 Bit und in der letzten für beide Architekturen. In der für 64 Bit sollten einige wenige Pakete genannt sein. Die für 32 Bit sollte leer sein und die für beide sollte den meisten Inhalt aufweisen. Da ich nur 64 Bit will habe ich daher einfach den Inhalt der Datei packages.both ausgeschnitten und unter den Inhalt der Datei packages.x86_64 eingefügt, so dass nun auch packages.both komplett leer ist. Die nun in der Datei packages.x86_64 genannten Pakete bzw. Paketgruppen sind quasi nur die Minimalinstallation. Hier kann man sich nach Lust und Laune austoben. Pro Zeile darf aber nur ein Paket bzw. eine Paketgruppe genannt werden. Fürs erste habe ich folgende Pakete/Gruppen hinzugefügt: lxde, meld, nano, xf86-video-ati, xf86-video-intel, xf86-video-nouveau, xf86-video-vesa, xorg-apps, xorg-server und xorg-server-utils. Auf eventuelle nötige Abhängigkeiten muss man hierbei nicht achten. Diese werden bei Bedarf automatisch installiert.

Da ich ohne eingreifen zu müssen automatisch lxdm und damit auch lxde ausführen möchte habe ich anschließend im Verzeichnis ~/archlive/releng/airootfs/etc/systemd/system folgenden Befehl ausgeführt: ln -s /usr/lib/systemd/system/lxdm.service display-manager.service. Das sollte eigentlich dem System mitteilen, dass lxdm automatisch gestartet wird. Erstellt man an dieser Stelle jetzt die Iso-Datei und bootet davon, wir man merken, dass es aber nicht klappt. Schuld ist hier die Datei customize_airootfs.sh welche man unter releng/airootfs/root findet. In dieser findet man die Zeile systemctl set-default multi-user.target. Und genau die verhindert dass lxdm automatisch gestartet wird. Quasi falscher Runlevel. Von daher habe ich das multi-user.target gegen graphical.target ausgetauscht. Da ich die Datei schon offen habe habe ich die Zeile "sed -i 's/#\(us_US\.UTF-8\)/\1/' /etc/locale.gen\" bei der Gelegenheit gleich auf "sed -i 's/#\(de_DE\.UTF-8\)/\1/' /etc/locale.gen" geändert.

Um zu verhindern, dass im Bootloader auch die Einträge für die 32-Bit-Version auftauchen habe ich weiterhin unter releng/syslinux alle Dateien mit 32 im Dateinamen (z. B. archiso_sys32.cfg) gelöscht. Abschließend habe ich nun in der Konsole das bereits erwähnte Script build.sh mittels ./build.sh -v ausgeführt. Der Parameter -v sorgt dafür dass der Vorgang etwas gesprächiger ist und man eventuelle Fehlerquellen bemerkt. Wenn alles geklappt hat, sollte man nun unter releng/out/ die Iso-Datei finden. Nach ersten Tests unter VirtualBox dürfte eigentlich alles geklappt haben. Lxdm sollte automatisch starten und man sollte sich problemlos an Lxde anmelden können. Für den bisher vorhandenen Nutzer ist aktuell übrigens kein Passwort gesetzt. Die wenigen vorhandenen Programme sollten eigentlich auch alle starten. Der Rohbau steht sozusagen.

Als nächstes werde ich wohl die Paketliste sowie das Startmenü von Lxde erweitern. Anregungen nehme ich gerne an.

Wer sich diese noch sehr eingeschränkte Live-Distribution einmal ansehen will, kann Sie unter [https://spideroak.com/browse/share/datengrab/Merkitys](https://spideroak.com/browse/share/datengrab/Merkitys  "https://spideroak.com/browse/share/datengrab/Merkitys") herunterladen. Die Prüfsummen sind wie folgt.

MD5: e08e6116dff6173c906a2b91714a4992
SHA256: 4dade41774bb1faaac12decac3796b2fd3299a5fb22314e5305846acd548db18

Vermutlich werden jetzt einige sich fragen wieso ich nicht einfach eine bereits fertige Live-Distribution wie die SystemRescueCD nehme. Im Grunde genommen will ich zwei Dinge damit erreichen. Zum einen will ich archiso bzw. das Remastern einer bereits vorhandenen Arch-Live-Distribution besser verstehen. Und zum anderen will ich testen inwiefern bei einer solchen Iso-Datei Delta-Updates (mit xdelta3 erstellt) Sinn machen.
