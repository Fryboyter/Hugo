---
title: Ausfall der Webseite und die Entdeckung von Pydio
date: 2013-11-13T13:35:00+0100
categories:
- OSBN
- Allgemein
tags:
- Layer 8
- Pydio
slug: ausfall-der-webseite-und-die-entdeckung-von-pydio
---
Heute ist für ein paar Stunden diese Seite nicht erreichbar gewesen. Der Grund war, dass mal wieder so ein Vollidiot gemeint hat, er müsse sein neues Spamtool mal bei mir ausprobieren. Da er so schlau war, das immer über die gleiche IP zu machen, wollte ich über das Plugin "Yoast WordPress SEO" die Datei .htaccess mal eben anpassen und ihn aussperren. Leider hat mir da ein kapitales Layer-8-Problem einen dicken Strich durch die Rechnung gemacht, so dass man für ein paar Stunden nur der [Fehler 500](http://de.wikipedia.org/wiki/Fehlerseite" "HTTP Fehlerseiten") angezeigt wurde.

Da ich, Firewall sei dank, keine SSH-Verbindung zu meinem Webspace aufbauen konnte, habe ich daher erst mal in die Röhre geschaut. Mein Mobiltelefon, auf dem ein SSH-Client installiert ist, lag natürlich auch daheim. Also doch noch schnell heim und es von dort aus reparieren. Man hat ja sonst nichts zu tun. Bei der Gelegenheit habe ich gleich mal Google gequält, wie ich solche Probleme in Zukunft einfacher lösen kann, ohne mich mit der Firewall anzulegen. Dabei bin ich auf [Pydio](http://pyd.io "Pydio") gestoßen. Genauer kann ich es mir erst heute Abend daheim ansehen. Aber bisher bin ich ziemlich begeistert. Ich würde es als Mischung zwischen Owncloud und einem Dateimanager bezeichnen, der man eine Priese Speed verpasst hat. Auf die Schnelle würde ich sagen, dass Ding bietet so ziemlich alles. Naja nicht alles, aber sehr viel wie WebDAV, Samba, Dropbox, LDAP/AD, Antivirus, Dateifreigaben, Benutzerverwaltung, EncFs, SFTP, Dateieditoren (ganz wichtig, falls ich mal wieder ein Layer-8-Problem habe) usw. usw. Genaueres findet man unter [http://pyd.io/plugins](http://pyd.io/plugins "Pydio Plugins").

Die Installation ist auch idiotensicher. Hochladen, aufrufen und dem Installationsprozess folgen. Die Konfiguration erfolgt entweder in einer Datei oder in einer Datenbank.

Clients für iOS und Android sowie ein Client zum Abgleichen (noch nicht stabil. Für Windows, Mac und Linux) der Dateien werden, wie auch einige Bridges (z. B. zu Wordpress) werden ebenfalls angeboten.

Sollten sich heute Abend nicht arge Nachteile herausstellen, werde ich Dropbox und Co. wohl einstampfen.

Wer sich mal ein Bild machen will, findet unter [https://demo.pyd.io](https://demo.pyd.io "Pydio Demo") eine Demoinstallation.