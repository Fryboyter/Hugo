---
title: Cache von Pacman automatisch aufräumen
date: 2018-04-07T09:20:57+0100
categories:
 - Linux
 - OSBN
tags:
- Arch
- Linux
- Pacman
- Cache
slug: cache-von-pacman-automatisch-aufraeumen
---
Der Paketmanager Pacman speichert die Pakete unter /var/cache/pacman/pkg. Um bei Problemen ein Downgrade machen zu können, werden dort automatisch keine Pakete entfernt.

Leert man das Verzeichnis nicht regelmäßig kann es sein, dass irgendwann die Festplatte voll ist und man sich wundert was nun schon wieder schief gegangen ist. Um dies zu vermeiden, kann man sich einen sogenannten Hook erstellen. Mit diesen lassen sich Aktionen bevor oder nachdem etwas mit Pacman gemacht wird ausführen.

Um bei dem Beispiel mit Cache zu bleiben, erstellen wir erst einmal das Verzeichnis /etc/pacman.d/hooks sofern es nicht schon vorhanden ist. In diesem erstellen wir dann eine Datei an deren Ende .hook stehen muss. Also beispielsweise pacman-cache-aufraeumen.hook. In diese kommt dann folgender Inhalt:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[Trigger]
Operation = Remove
Operation = Install
Operation = Upgrade
Type = Package
Target = *

[Action]
Description = Cache von Pacman aufräumen...
When = PostTransaction
Exec = /usr/bin/paccache -rqk2</code>
</pre>

Im Bereich Trigger wird definiert in welchem Fall das ganze ausgeführt werden soll und für was der Hook gültig ist. in diesem Fall wird also die Aktion beim Entfernen, Installieren und Aktualisieren aller Pakete ausgeführt.

Im Bereich Action wird angegeben, was ausgeführt wird und wann. In diesem Beispiel wird der Befehl /usr/bin/paccache -rqk2 nach dem Entfernen, Installieren oder Aktualisieren eines Pakets ausgeführt. Der Parameter -rqk2 bewirkt, dass alle Pakete im Cache bis auf die letzten zwei Versionen entfernt werden und dass dies ohne Rückmeldung geschieht.
