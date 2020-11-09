---
title: Suchanfrage direkt an die eigene Searx-Installation schicken
date: 2017-09-26T15:09:00+0100
categories:
- Linux
- OSBN
tags:
- Searx
- Suchanfragen
slug: suchanfrage-direkt-an-die-eigene-searx-installation-schicken
---
Ich habe mir angewöhnt im Browser Suchanfragen über Kürzel zu stellen. Somit suche ich beispielsweise mit "g wayland arch linux" nach Wayland unter Arch Linux. Oder mit "ddg hamburger teespeicher" suche ich mit DuckDuckGo nach meinem bevorzugten Teehändler dem Hamburger Teespeicher. Nur meine Searx-Instanz habe ich bisher direkt aufgerufen.

Das habe ich jetzt einmal geändert und mir für meine eigene Searx-Instanz ebenfalls einen Suchmaschineneintrag erstellt. Im Grunde genommen ist es kein Hexenwerk und in unter einer Minute erledigt.

{{< image src="searxsuche.png" alt="Searx Suche" >}}

Dieses Beispiel zeigt das Hinzufügen einer Suchmaschine unter Vivaldi (ALT+P -&gt; Suche). Unter Chrome/Chromium sollte es vermutlich gleich bzw. ähnlich aussehen. Zu anderen Browsern kann ich keine Aussage treffen.

Als URL geben wir die Adresse ein, unter der die betreffende Searx-Instanz erreichbar ist. An deren Ende fügen wir dann noch /?q=%s hinzu. Das %s ist hier ein Platzhalter für unsere Suchbegriffe. Als Kürzel habe ich mal sx genommen, da "s" bereits für Startpage vorgesehen ist. Abschließend noch schnell auf Hinzufügen klicken und fertig. Wer will, kann vorher den Eintrag als Standard setzen. Nun kann man direkt in der Adresszeile mit dem Kürzel sx eine Searx-Installation befragen.

Searx bietet auch die Möglichkeiten diverse Kategorien zu durchsuchen. Wie zum Beispiel unter anderem Nachrichten, Musik, IT oder Dateien. Nehmen wir mal an, dass man einen Eintrag für die Kategorie "Nachrichten" erstellen will. Hierzu müssen wir obigen Link einfach erweitern, so dass aus http://searx.fryboyter.de/?q=%s&amp;categories=news wird. Anstelle von news trägt man hier einfach die gewünschte Kategorie ein. Hierzu muss man allerdings die englische Bezeichnung nutzen.

Ach ja... Der genannte Link ist nur ein Beispiel und funktioniert nicht. Wer sich die Metasuchmaschine einmal ansehen will, findet unter [https://github.com/asciimoo/searx/wiki/Searx-instances](https://github.com/asciimoo/searx/wiki/Searx-instances) eine Liste von Instanzen. Hier dürfte searx.me mit die bekannteste Adresse sein. Für die Installation einer eigenen Instanz lohnt sich ein Blick in die [Anleitung](https://blog.mdosch.de/2017/08/28/searx-auf-uberspace-einrichten) von mdosch. Diese ist zwar für Uberspace gedacht, aber ich denke man hiermit auch Searx bei anderen Anbietern installieren.
