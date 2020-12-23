---
title: Benachrichtigungen von Isso ohne Betreff
date: 2018-05-04T17:48:16+0100
categories:
- OSBN
- Allgemein
tags:
- Isso
- Benachrichtigungen
- Betreff
slug: benachrichtigungen-von-isso-ohne-betreff
---
Da sich auf fryboyter.de einige menschliche Spambots herumtreiben ist Isso bei mir so eingestellt, dass ich für jeden neuen Kommentar eine E-Mail erhalte in dem dann ein Link zum Freischalten bzw. Löschen des Kommentars enthalten ist. Der Betreff dieser E-Mails war bei mir immer leer. Da ich die Kommentare aber problemlos moderieren konnte war mir das bisher egal. Naja eigentlich ist es mir immer noch egal.

Aufgrund des [Commento-Artikels](/alternative-zu-isso/ "Commento-Artikels") und des Kommentars von mdosch wegen der Datenübernahme von Isso habe ich mir eben einmal die Datenbankstruktur von Isso angesehen, weil ich morgen mal versuchen will ob ich es gebacken bekomme die Daten von Isso zu Commento zu portieren. In der Isso-Datenbank gibt es die Tabelle threads. In dieser ist die Spalte title vorhanden. Bei jedem Artikel den ich unter Bolt CMS erstellt habe und bei dem es Kommentare gibt ist hier die Spalte leer. Keine Ahnung wie Isso hier versucht den Titel des Artikels herauszufinden aber scheinbar klappt das bei mir nicht. Eventuell weil ich für die Titel den HTML-Tag H2 und nicht H1 nutze.

Auch wenn ich durch den fehlenden Betreff keine Nachteile habe, habe ich mich daran festgebissen. Die Lösung ist im Grunde aber in meinem Fall ganz einfach. Bisher wurde Isso wie folgt eingebunden:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-php">&lt;section&gt;
    &lt;h3&gt;Kommentare&lt;/h3&gt;
    &lt;section id=&quot;isso-thread&quot;&lt;/section&gt;
&lt;/section&gt;</code>
</pre>

In der Dokumentation von Isso findet man hier die Möglichkeit mit data-title="" einen Titel vorzugeben. Das jedes mal manuell zu machen ist mir dann doch zu blöd. Twig sei Dank ist die Lösung aber trivial. Anstelle des Titels habe ich einfach {{ record.title }} eingetragen, so dass das ganze nun wie folgt aussieht.


<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-php">&lt;section&gt;
   &lt;h3&gt;Kommentare&lt;/h3&gt;
   &lt;section id=&quot;isso-thread&quot; data-title=&quot;{{ record.title }}&quot;&gt;&lt;/section&gt;
&lt;/section&gt;</code>
</pre>

Damit wir nun die Spalte title befüllt und die E-Mails haben auch einen Betreff. Wenn nur alle Problem so leicht zu lösen wären. Vielleicht klappt der Import der Isso-Kommentare in Commento ja auch so einfach. Man darf ja noch träumen, oder?
