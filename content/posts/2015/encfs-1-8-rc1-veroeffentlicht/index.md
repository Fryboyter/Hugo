---
title: EncFS 1.8 RC1 veröffentlicht
date: 2015-01-13T14:44:00+0100
categories:
- Linux
- OSBN
tags:
- EncFS
- Audit
slug: encfs-1-8-rc1-veroeffentlicht
---
Wenn es um das Verschlüsseln von Daten bei Cloud-Anbietern wie Dropbox geht, habe ich ganz gerne EncFS genutzt, da der Zugriff nicht nur unter Linux sondern auch unter Windows möglich ist. Anfang 2014 hat sich Taylor Hornby die Mühe gemacht und hat EncFS auf Sicherheitslücken untersucht. Da die letzte offizielle Version von Ende 2011 war und sich seit dem auch einige Dinge in Sachen Sicherheit getan haben, hat er natürlich einige Probleme [gefunden](https://defuse.ca/audits/encfs.htm "EncFS Security Audit") und dem Entwickler gemeldet. Dieser hat die Aussage getroffen, dass Version 2.0 in Entwicklung ist und dass die Behebung der Probleme dort mit einfließen wird. Und dann war Stille. Bis vor ein paar Tagen.

Am 06.01.15 wurde EncFS 1.8 RC1 veröffentlicht. Bei der Gelegenheit ist das Projekt auch zu [Github](https://github.com/vgough/encfs "EncFS") umgezogen. Laut dem Entwickler bietet der neue RC folgende Highlights.

- improve automatic test converage: also test reverse mode (make test)
- add per-file IVs based on the inode number to reverse mode to improve security
- add automatic benchmark (make benchmark)
- compare MAC in constant time ( fixes bug #12 )
- add --nocache option
- lots of fixes to make building on OSX easier

Somit dürfen schon mal zwei Sicherheitsprobleme behoben sein. Ich hoffe, dass die Entwicklung von EncFS nun nicht wieder einschläft und man das Tool zukünftig wieder ohne ein ungutes Gefühl im Hinterkopf benutzten kann.
