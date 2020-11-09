---
title: Autokorrektur der ZSH partiell zum Schweigen bringen
date: 2018-01-04T11:28:00+0100
categories:
- Linux
- OSBN
tags:
- ZSH
- Autkorrektur
slug: autokorrektur-der-zsh-partiell-zum-schweigen-bringen
---
Gestern habe ich alle wichtigen Dienste von Uberspace V6 auf Uberspace V7 verschoben. So wie es aussieht, hat wohl alles geklappt. Allerdings ging mit die Autokorrektur der ZSH auf die Nerven.

Da mir Befehle wie "ssh nutzer@planet.uberspace" zu umständlich sind, habe ich in der ~/.ssh/config [Einträge](https://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix) angelegt, so dass ich mich beispielsweise mittels "ssh uberspace6" auf meinen Uberspace6 einwählen kann. Vor kurzem kam hier noch der Eintrag für uberspace7 hinzu. Wenn ich nun "ssh uberspace7" ausführen wollte, hat mich die Autokorrektur der ZSH jedes mal gefragt, ob ich nicht Uberspace gemeint habe. Nein verdammt, habe ich nicht. Das ging mir mit der Zeit auf den Zeiger. Eine komplette Deaktivierung der Korrektur für die Parameter wollte ich aber auch nicht. Daher habe ich mir den Alias ssh='nocorrect ssh' erstellt. Damit verkneift sich die Korrektur die Fragen und ich habe meine Ruhe. Dank der Vervollständigungsfunktion bzw. History-Funktion entstehen in dem Fall auch keine Problem und man kann schnell zwischen zwei ähnlichen Einträgen auswählen. Solch ein Alias lässt sich auch für jeden anderen Befehl anlegen.
