---
title: 'E-Mail-Adressen mit Python aus Datenbanksicherung auslesen'
date: '2016-12-05 19:58:00'
categories:
- Linux
- OSBN
tags:
- MySQL
- Email
- Python
slug: e-mail-adressen-mit-python-aus-datenbanksicherung-auslesen
---
Ab und zu werde ich bei schwierigen Fällen um Hilfe gebeten. Wie zum Beispiel vor ein paar Tagen. Aufgabenstellung war, die E-Mail-Adressen in einer MySQL-Datenbank zu finden und die Treffer in eine Textdatei zu schreiben. Das Problem ist aber, dass die Datenbank nur als Datensicherung in Form einer SQL-Datei vorliegt und diese nicht eingespielt werden soll oder kann. Wäre auch zu einfach gewesen.

Da ich gerade als Fachliteratur das eBook von "Automate the Boring Stuff with Python" lese habe ich mich für Python als Lösung entschieden. Herausgekommen ist folgendes "Kunstwerk".

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-python">#!/usr/bin/env python
""" Emails in einer Datei finden und Treffer in eine neue Datei schreiben """

import os
import re

QUELLDATEI = input("Quelldatei angeben: ")
ZIELDATEI = input("Zieldatei angeben: ")

if os.path.exists(QUELLDATEI):
    DATEN = open(QUELLDATEI, 'r')
    EMAILDATEI = DATEN.read()
else:
    print("Datei nicht gefunden")
    raise SystemExit


# Regex und Suche ohne doppelte Treffer
EMAILREGEX = re.compile(
    r'[a-z0-9!#$%&*+=?^_`{|}~-]+(?:\.[a-z0-9!#$%&*+=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?', re.IGNORECASE)
TREFFERDOPPELT = EMAILREGEX.findall(EMAILDATEI)
TREFFEREINFACH = set(TREFFERDOPPELT)

# Treffer ausgeben und in Datei schreiben
with open(ZIELDATEI, 'w') as f:
    for row in TREFFEREINFACH:
        print(row)
        f.write("%s\n" % str(row))</code>
</pre>

Habe ich schon erwähnt, dass ich so gut wie gar nicht programmieren kann? Nein? Gut ich kann es so gut wie nicht. Aber erstaunlicherweise funktioniert es. Auf eine Prüfung ob die jeweilige E-Mail-Adresse gültig ist, habe ich bewusst verzichtet. Das wird mit RegEx sonst ein Fass ohne Boden. Vor allem weil ich RegEx noch weniger beherrsche als z. B. Python. Von daher wie immer... Benutzung auf eigene Gefahr.

**Nachtrag:**
Nach einem Testlauf ist mir aufgefallen, dass einige Adressen mehrfach vorhanden sind. Ich habe das Script daher noch einmal angepasst, so dass nun keine doppelten Adressen ausgegeben werden.

**Nachtrag 2**
Ich habe das Script noch einmal angepasst. Zum einen wird nun die Quelldatei sowie die Zieldatei abgefragt und ist nicht mehr fest hinterlegt und zum anderen habe ich mich an den PEP8-Richtlinien (außer der Zeilenlänge) orientert.
