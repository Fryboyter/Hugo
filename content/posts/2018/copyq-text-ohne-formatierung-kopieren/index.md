---
title: CopyQ - Text ohne Formatierung kopieren
date: 2018-09-11T12:47:00+0100
categories:
- Linux
- OSBN
tags:
- CopyQ
- Kopieren
slug: copyq-text-ohne-formatierung-kopieren
---
Wie vor kurzem schon [angemerkt](/ausnahmen-fuer-copyq-erstellen/), nutze ich für die Zwischenablage nun CopyQ. Im Grunde bin ich damit zufrieden, aber es stört mich, dass der Text immer inkl. eventuell vorhandener Formatierungen kopiert wird. Leider gibt es in den Einstellungen keine Möglichkeit dies abzustellen.

CopyQ bietet allerdings die durchaus mächtige Funktion an, neue Befehle zu erstellen. Mit diesem lassen sich auch vorhandene Befehle überschreiben. Wie eben das Kopieren von Text. Hierfür ist folgender Code nötig.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[Command]
Automatic=true
Command="
    copyq:
    if (dataFormats().indexOf(mimeHtml)) {
      removeData(mimeHtml)
      copy(mimeText, data(mimeText))
    }"
Icon=\xf031
Input=text/plain
Name=HTML ignorieren</code>
</pre>

Diesen kopiert man einfach und öffnet dann in CopyQ mittels F6 (alternativ Datei -&gt; Befehle/Globale Tastenkombinationen...) das Fenster in dem man die Befehle erstellen kann. Dort findet man rechts unten die Schaltfläche "Befehle einfügen [Strg+V]". Klickt man darauf wird der eben kopierte Code eingefügt. Anschließend klickt man noch auf OK und das war es schon. Von nun an wird jeder Text ohne Formatierungen in die Zwischenablage eingefügt.
