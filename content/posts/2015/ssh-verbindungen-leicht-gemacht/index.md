---
title: SSH-Verbindungen leicht gemacht
date: 2015-04-23T19:09:00+0100
categories:
- Linux
- OSBN
tags:
- SSH
- Verbindung
- Alias
slug: ssh-verbindungen-leicht-gemacht
---
Ich nutze regelmäßig SSH-Verbindungen zu diversen Rechnern. Im LAN z. B. zu meinem Receiver oder zu meinem Quake-3-Arena-Server. Da letzterer im Internet erreichbar ist, läuft SSH nicht auf dem Standardport sondern auf einen anderen um Scriptkiddies zu blocken und somit die Logdateien sauber zu halten. Somit muss ich jedes mal, wenn ich mich mit dem Rechner verbinden will ssh $Benutzer@$IP -p $Portnummer -i ~/.ssh/quake eingeben. Oder den Befehl aus der Historie von ZSH herausfischen. Das muss doch auch besser funktionieren, oder? Ja tut es.

Hierzu legt man, falls nicht schon vorhanden, als erstes die Datei ~/.ssh/config auf dem Rechner mit dem man sich mit dem Server verbinden will an. Nun erstellt man in dieser folgenden Eintrag.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">Host quake
Hostname 192.168.1.220
Port 1234
User quake
IdentityFile /home/$Benutzer/.ssh/quake</code>
</pre>

In der ersten Zeile geben wir den Namen der Verbindung an. Hier kann man frei wählen. Als nächstes geben wir die IP des Rechners an zu dem wir uns verbinden möchten. Der Port muss angegeben werden, wenn wir einen, vom Standard abweichenden, Port eingestellt haben. In der nächsten Zeile wird der Benutzer angegeben mit dem wir uns auf dem Rechner einloggen möchten. Sollte man anstelle von Passwörtern SSH-Keys nutzen und hat man mehrere unter ~/.ssh liegen gibt man am besten mit IdentityFile auch noch die richtige Schlüsseldatei an.

Nachdem man die Datei abgespeichert hat, braucht man nun nicht mehr ssh $Benutzer@$IP -p $Portnummer -i ~/.ssh/quake eingeben sondern es reicht ganz bequem ssh quake.
