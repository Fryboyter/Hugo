---
title: Prosody bei uberspace.de installieren
date: 2012-08-26T21:02:00+0100
categories:
- Linux
- OSBN
tags:
- XMPP
- Jabber
- Prosody
slug: prosody-bei-uberspace-de-installieren
---
Jetzt habe ich es endlich mal in Angriff genommen, und versucht, den XMPP-Server Prosody auf meinem Uberspace zu installieren. Als erstes habe ich mit per SSH eingeloggt. Das hat schon mal funktioniert... ;-) Als nächstes habe ich mir den Source-Code heruntergeladen und diesen dann entpackt.

>wget http://prosody.im/downloads/source/prosody-0.8.2.tar.gz

>tar xzf prosody-0.8.2.tar.gz

Da mich Versionsnummern im Verzeichnisnamen nerven, habe ich noch schnell das Verzeichnis umbenannt und bin dann in das Verzeichnis gewechselt.

>mv prosody-0.8.2 prosody

>cd prosody

Laut Anleitung reicht ein **./configure** aus. Hier habe ich mir überlegt, wann ich das zum letzten mal gemacht habe. Ist auf jeden Fall lange her. Da ich aber vermutlich keinen Vollzugriff auf alle Verzeichnisse habe, habe ich daraus erst einmal ein **./configure --prefix=/home/benutzer/prosody** gemacht, damit das ganze im Homeverzeichnis installiert wird. Und schon bekam ich die erste Fehlermeldung um die Ohren.

>./configure --prefix=/home/mathmos/prosody Lua interpreter found: /usr/bin/lua... Looking for Lua... Checking Lua includes... lua.h not found (looked in /usr/include/lua.h) You may want to use the flag --with-lua-include. See --help.

Er findet also die Datei lua.h nicht unter /urs/include/. Langsam habe ich mich wieder erinnert, wieso ich diese Installationsart schon ewig nicht mehr verwendet habe. Genau wegen solchen Sachen. Unter anderem. Also habe ich mir mal das Wiki von uberspace.de angesehen, was dort zum Thema LUA steht. Wenige Sekunden später hatte ich die Lösung. Das Zeug liegt hier unter /package/host/localhost/lua/. Dort gibt es dann ein Unterverzeichnis include in der die benötigte Datei liegt. Was sagt uns ./configure --help zu dem Thema? Eigentlich alles was man braucht. Also nächster Versuch...

>./configure --prefix=/home/mathmos/prosody --with-lua-include=/package/host/localhost/lua/

Damit sollte lua.h nun zu finden sein. Und genau so war es dann auch. Das ganze lief ohne Probleme durch. Also gleich ein **make** hinterher. Auch das hat funktioniert. Jetzt wollte ich den Server zumindest einmal zum testen starten. Also gleich mal das Teil mittels **./prosody** aufgerufen. Und was soll ich sagen. Es funktioniert nicht, weil der Server einige LUA-Erweiterungen [nicht findet](http://pastebin.com/WSsKk5k8 "Fehlermeldung Prosody"). Da ich die vermissten Sachen auch nicht gefunden habe, habe ich gerade eine Anfrage an hallo@uberspace gestellt. Mit etwas Glück wird es nachgerüstet. Mit etwas Pech muss ich die Sachen selbst ins Homeverzeichnis installieren. Mit etwas mehr Pech funktioniert das nicht. Aber ich warte jetzt erst mal die Antwort ab.
