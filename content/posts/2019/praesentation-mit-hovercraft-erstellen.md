---
title: Präsentation mit Hovercraft erstellen
date: 2019-01-13T14:54:00+0100
categories:
- Linux
- OSBN
tags:
- Hovercraft
- Präsentationen
slug: praesentation-mit-hovercraft-erstellen
---
Ich habe mich leider mal wieder breitschlagen lassen eine Präsentation zu halten, obwohl ich es hasse. Um nicht schon bei der Erstellung der Präsentation als nervliches Wrack zu enden, nutze ich [Hovercraft](https://github.com/regebro/hovercraft).

Hiermit erstellt man mittels reStructuredText Impress.js-Präsentationen. Somit kann eine Seite der Präsentation zum Beispiel wie folgt aussehen.

<pre>
<code class="language-bash">The problem:
============

Making presentations is no *fun!*
---------------------------------

.. note::

    Welcome to the presenter console!

----</code>
</pre>

Das ganze ist also ziemlich idiotensicher. Bei Fragen lohnt sich ein Blick in die offizielle [Dokumentation](https://hovercraft.readthedocs.io/en/latest/index.html). Ist man mit seiner Präsentation fertig, erstellt man mittels "hovercraft Hovercraft-Datei Zielverzeichnis" einfach die Präsentation im HTML5-Format, welche im Grunde genommen mit jedem halbwegs aktuellen Browser anzeigbar ist.

Damit man sich einen visuellen Überblick verschaffen kann, bieten die Entwickler von Hovercraft eine [Demo-Präsentation](http://regebro.github.com/hovercraft) an.

Wer die Präsentation den Teilnehmern als PDF-Datei zur Verfügung stellen will, kann dies zum Beispiel mit [rst3pdf](https://github.com/rst2pdf/rst2pdf) machen.
