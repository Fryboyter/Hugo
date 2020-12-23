---
title: Record.twig des Fryboyter-Themes
date: 2017-07-05T07:00:00+0100
categories:
- OSBN
- Allgemein
tags:
- Bolt CMS
slug: record-twig-des-fryboyter-themes
---
In meinem letzten [Artikel](/index-twig-des-fryboyter-themes/) habe ich die Datei index.twig meines Twig-Themes erklärt. Jetzt ist die Datei record.twig an der Reihe. Diese ist teilweise identisch mit der index.twig.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-twig">{% include '_header.twig' %}
&lt;div class=&quot;header&quot;&gt;&lt;h1&gt;&lt;a href=&quot;{{ paths.hosturl }}&quot;&gt;Fryboyter&lt;/a&gt;&lt;/h1&gt;&lt;/div&gt;
    &lt;div class=&quot;container&quot;&gt;
        &lt;div class=&quot;row&quot;&gt; 
            &lt;div class=&quot;col-lg-8 col-lg-offset-2 col-md-10 col-md-offset-1&quot;&gt;
                    &lt;h2&gt;{{ record.title }}&lt;/h2&gt;
                    {% if record.taxonomy is defined %}
                        {% for type, values in record.taxonomy %}
                            &lt;div class=&quot;article-info&quot;&gt;Ver&ouml;ffentlicht am {{ record.datepublish|localdate(&quot;%d. %B %Y&quot;) }} unter:
                        {% for link, value in values %}
                            &lt;a href=&quot;{{ link }}&quot;&gt;{{ value }}&lt;/a&gt;{% if not loop.last %} &amp; {% endif %}
                        {% endfor %}
                            | &lt;a href=&quot;{{ record.link }}#isso-thread&quot;&gt;Comments&lt;/a&gt;
                        {% if user.id is defined %}
                        {% if user.id == 'X' %}
                            | &lt;a href=&quot;{{ paths.bolt }}editcontent/entries/{{ record.id }}&quot;&gt;Bearbeiten&lt;/a&gt;
                        {% endif %}
                        {% endif %} 
                        {% endfor %}
                    {% endif %}&lt;/div&gt;
                    {{ record.body }}                        
                    &lt;p&gt;Diese Artikel k&ouml;nnten auch interessant sein&lt;/p&gt;
                    &lt;ul&gt;{% setcontent records = &quot;entries/random/5&quot; allowpaging %}
                    {% for record in records %}
                    &lt;li&gt;&lt;a href=&quot;{{ record.link }}&quot;&gt;{{ record.title }}&lt;/a&gt;&lt;/li&gt;
                    {% endfor %}&lt;/ul&gt;
                    &lt;section&gt;
                        &lt;h3&gt;Kommentare&lt;/h3&gt;
                        &lt;section id=&quot;isso-thread&quot;&gt;&lt;/section&gt;
                    &lt;/section&gt;
        &lt;/div&gt; 
    &lt;/div&gt;   
&lt;/div&gt;
&lt;div class=&quot;footer&quot;&gt;{% include '_footer.twig' %}&lt;/div&gt;</code>
</pre>

Den ersten Unterschied findet man in Zeile 14 bis 18. Hier wird als erstes geprüft, ob die Variable user.id definiert ist. Wenn dies der Fall ist erfolgt die Prüfung, ob der Nutzer die Nutzer-ID X hat. Wenn ja, wird die Zeile in der das Datum der Veröffentlichung, die Kategorien sowie die Kommentare angezeigt wird um einen weiteren Link erweitert mit dem man den betreffenden Beitrag ändern kann.

Zeile 22 bis 26 erstellt eine Liste von 5 zufälligen Artikeln, die eventuell für den Leser auch interessant sein könnten und gibt deren Titel aus die auf die einzelnen Artikel verlinken. Hier werden aktuell noch Artikel kategorieübergreifend angezeigt. Geplant habe ich hier, dass nur Artikel angezeigt werden, die den gleichen Kategorien zugeordnet sind, wie der aufgerufene Artikel.

Zeile 27 bis 30 bindet die Kommentarfunktion von Isso Comment ein.
