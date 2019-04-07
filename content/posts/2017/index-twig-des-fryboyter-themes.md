---
title: Index.twig des Fryboyter-Themes
date: 2017-07-04T09:10:18+0100
categories:
- OSBN
- Allgemein
tags:
- Fryboyter
- Theme
- Bolt CMS
slug: index-twig-des-fryboyter-themes
---
Da ich gefragt wurde, wie ich das auf fryboyter.de verwendet Theme erstellt habe, habe ich mir gedacht ich mache mal eine Artikelreihe daraus in der ich die 9 Twig-Dateien erkläre.

Fangen wir mal mit der Datei index.twig an. Diese wird angezeigt, wenn man die Hauptseite aufruft.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-twig">{% include '_header.twig' %}
&lt;div class=&quot;header&quot;&gt;&lt;h1&gt;&lt;a href=&quot;{{ paths.hosturl }}&quot;&gt;Fryboyter&lt;/a&gt;&lt;/h1&gt;&lt;/div&gt;
&lt;div class=&quot;container&quot;&gt;
    &lt;div class=&quot;row&quot;&gt;
        &lt;div class=&quot;col-lg-8 col-lg-offset-2 col-md-10 col-md-offset-1&quot;&gt;
            {% setcontent records = &quot;entries/latest/5&quot; allowpaging %}
                {% for record in records %}
                    &lt;h2&gt;&lt;a href=&quot;{{ record.link }}&quot;&gt;{{ record.title }}&lt;/a&gt;&lt;/h2&gt;
                        {% if record.taxonomy is defined %}
                            {% for type, values in record.taxonomy %}
                            &lt;div class=&quot;article-info&quot;&gt;Ver&ouml;ffentlicht am {{ record.datepublish|localdate(&quot;%d. %B %Y&quot;) }} unter:
                            {% for link, value in values %}
                            &lt;a href=&quot;{{ link }}&quot;&gt;{{ value }}&lt;/a&gt;{% if not loop.last %} &amp; {% endif %}
                            {% endfor %}
                            | &lt;a href=&quot;{{ record.link }}#isso-thread&quot;&gt;Comments&lt;/a&gt; &lt;/div&gt;
                            {% endfor %}
                        {% endif %}
                    {{ record.body }}
                    &lt;hr/&gt;
                {% endfor %}
            {{ pager('', 3, '_sub_mypager.twig') }}
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;
&lt;div class=&quot;footer&quot;&gt;{% include '_footer.twig' %}&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</code>
</pre>

Twig bietet die Möglichkeit bestimmte Bereich einer Seite in extra Dateien auszulagern. Mittels include kann man diese dann wie im Baukasten zusammensetzen. In diesem Fall wird in Zeile 1 somit die Datei _header.twig importiert.

In Zeile 2 wird mittels path.hosturl auf die Adresse der Seite verlinkt. In dem Fall also https://fryboyter.de/. Zieht man die Seite irgendwann man auf eine andere Domain um, braucht man hier die Adresse nicht händisch ändern.

In Zeile 6 werden die letzten 5 Einträge aus der Datenbank herausgefischt. Allowpaging ermöglicht es, dass man am Ende einer Seite auf weitere Seiten mit wiederrum 5 Artikeln wechseln kann.

Ab Zeile 7 wird definiert wie jeder einzelne Artikel angezeigt wird.

In Zeile 8 wird als erstes der Titel inkl. entsprechenden Link eines Artikels ausgegeben.

Zeile 9 bis 17 ist schon etwas aufwändiger. Hier wird erst einmal geprüft ob dem betreffende Artikel Taxonomien zugeordnet wurden. Auf dieser Seite wären das die Kategorieren wie osbn oder Allgemein. Wenn dem so ist, wird unter der Zeile der Artikelüberschrift das Datum der Veröffentlichung, gefolgt von den zugeordneten Kategorien angezeigt. Die Anzeige der Kategorien erfolgt hierbei in einer Schleife, so dass zwischen den Kategorien ein &amp; angezeigt wird. Zum Schluss wird am Ende noch die Anzahl der vorhandenen Kommentare angezeigt und auf die Kommentarfunktion verlinkt (Zeile 18).

In Zeile 21 wird dann der Haupttext des Artikels angezeigt (ich arbeite nie mit Teasern).

Zeile 24 bindet die Datei _sub_mypager.twig ein. Hiermit wird am Ende einer Seite der Umschalter angezeigt mit dem man die Seiten wechseln kann.

Abschließend wird in Zeile 28 die Datei _footer.twig importiert.
