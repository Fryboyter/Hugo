---
title: Versionsverwaltung mit Fossil
date: 2018-12-04T20:42:43+0100
categories:
- OSBN
- Allgemein
tags:
- Versionsverwaltung
- Fossil
slug: versionsverwaltung-mit-fossil
---
Bisher habe für meine privaten Projekte immer vermieten eine Versionsverwaltung zu verwenden. Da ich Ende des Monats mein Ansible-Projekt umsetzen werde und ein weiteres größeres Projekt geplant ist ist es wohl Zeit für solch ein Tool.

Die meisten werden vermutlich keinen Gedanken daran verschwenden und den Platzhirsch git nutzen. Ich kann mich mit git aber nicht anfreunden. Und vom Funktionsumfang werde ich vermutlich nur einen Bruchteil benötigen. Also mache ich, was ich ganz gut kann. Mir alternative Programme ansehen.

Da ich in einer Kathedrale und nicht auf einem Basar entwicklen werde, habe ich mich spontan für Fossil entschieden. Dieses Tool wird zum Beispiel für die Entwicklung von SQLite verwendet. Zudem sind die Entwickler von SQLite zufällig auch die Entwickler von Fossil. Warum das so ist, kann man unter https://sqlite.org/whynotgit.html nachlesen.

Auch wenn die Bedienung von Fossil Ähnlichkeiten mit der von git aufweist, finde ich Fossil angenehmer zu bedienen.

<pre>
<code class="language-bash">fossil init ansible #Repository "ansible" erstellen
nfossil open ansible #Repository "ansible" öffnen
fossil add install.yml #Datei "install.yml" zum Repository hinzufügen
fossil commit #Änderung bestätigen
fossil close ansible #Repository "ansible" schließen</code>
</pre>

Fossil bietet natürlich noch weitere Möglichkeiten. Genaueres kann man in der [Dokumentation](https://fossil-scm.org/index.html/doc/trunk/www/permutedindex.html) nachlesen. Aber Moment... Warum wird bei obigen Beispiel das Repository geöffnet und geschlossen. An dem Punkt kommen wir zur Besonderheit von Fossil. Ein Repository wird hier in eine SQLite-Datenbank gepackt. Somit wird mit "open" die Verbindung aufgebaut und mit "close" geschlossen. Auf den ersten Blick mit sqlitebrowser macht der Datenbankaufbau keinen schlechten Eindruck.

Abschließend möchte ich noch anmerken, dass Fossil auch über einen grafische Oberfläche verfügt, über die unter anderem eine Timeline der Änderungen, ein Forum und ein Wiki angeboten werden. Im Grunde wie bei Github. Wie das genau aussieht kann man sich auf der [offiziellen Seite](https://fossil-scm.org) von Fossil ansehen. Diese läuft mit besagter Oberfläche. Lokal lässt sich diese mit "fossil ui ansible" starten, so dass man das ganze auch einzelner Entwickler intern nutzen kann.