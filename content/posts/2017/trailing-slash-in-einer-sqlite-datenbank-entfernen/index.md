---
title: Trailing Slash in einer SQLite-Datenbank entfernen
date: 2017-02-01T22:13:00+0100
categories:
- Linux
- OSBN
tags:
- Slash
- SQlite
slug: trailing-slash-in-einer-sqlite-datenbank-entfernen
---
Sehr langsam aber sicher schreitet mein Umstieg von Wordpress auf Bolt CMS voran. Eine weitere Hürde habe ich eben überwunden. Den Import vorhandener Kommentare in ISSO Comments.

Die Zuordnung der Kommentare zu den Artikeln erfolgt über den Titel des Artikels. So ist beispielsweise in der Isso-Datenbank /archlinux-org-schafft-beginners-guide-ab/ gespeichert. Allerdings wurde beim betreffenden Artikel keine Kommentare angezeigt. Wie so oft liegt der Fehler im Detail...

Bolt CMS entfernt automatisch den Slash (trailing slash) am Ende eines Links. Somit lautet der Link unter Bolt dann https://fryboyter.de/archlinux-org-schafft-beginners-guide-ab. So ohne weiteres lässt sich dies wohl auch nicht abstellen, da die Funktion in einer der Core-Dateien vorhanden ist. Und da das eben ein anderer Link ist, zeigt Isso Comments somit auch nichts an. Ich habe kurzerhand einfach den trailing slash auch in der SQLite-Datenbank von Isso Comments entfernt. Hierzu war nur folgender, kurzer Befehl nötig.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-sql">UPDATE threads SET uri = rtrim(uri, '/')</code>
</pre>

Hier wird einfach beim Titel der Slash rechts am Ende entfernt. Und schon tauchen auch die Kommentare unter den Artikeln auf.
