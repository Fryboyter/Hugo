---
title: Datum in Sublime Text einfügen
date: 2019-04-27T22:46:29+0200
categories: 
- OSBN
- Allgemein
tags:
- Sublime Text
- Datum
- Hugo
slug: datum-in-sublime-text-einfuegen
---
Erstellt man einen Artikel mit Hugo gibt man in der Markdown-Datei das Datum in Form von 2019-04-27T22:18:13+0200 an. Im Gegensatz zu [Jörg](https://blog.jkip.de/fuer-pcmanfm-als-datumsformat-iso-8601-einstellen/) nervt mich das aber ziemlich. 

Daher habe ich mir überlegt, wie ich die Eingabe automatisieren kann. Für meinen bevorzugten Editor Sublime Text gibt es hierfür das Plugin [InsertDate](https://packagecontrol.io/packages/InsertDate). Nach der Installation wählt man die richtige Zeitzone aus. Danach legen man sich am besten noch einen Shortcut an, mit dem man das Datum einfügt. Hierfür wählt man im Menü "Preferences" den Punkt "Key Bindings" aus. Im rechten Fenster trägt man nun folgenden Code zwischen die eckigen Klammern ein und speichert die Datei.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{ "keys": ["shift+f5"], "command": "insert_date", "args": {"format": "%Y-%m-%dT%H:%M:%S%z"} },
</code>
</pre>

Anstelle von shift+f5 kann man auch einen andere Tastenkombination verwenden. Von nun an fügt man mit dem definierten Shortcut das aktuelle Datum inklusive Uhrzeit und der Differenz zu UTC im ISO 8601 Format ein.