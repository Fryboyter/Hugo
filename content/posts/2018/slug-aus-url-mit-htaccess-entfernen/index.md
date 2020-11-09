---
title: Slug aus URL mit htaccess entfernen
date: 2018-02-17T19:47:00+0100
categories:
- Linux
- OSBN
tags:
- Bolt CMS
- Slug
- Htaccess
slug: slug-aus-url-mit-htaccess-entfernen
---
Normalerweise haben die Links auf Artikel mit Bolt CMS den Aufbau https://fryboyter.de/entry/Titel-des-Artikels. Die habe ich mittels der Routingfunktion auf https://fryboyter.de/Titel-des-Artikels umgebogen. Soweit so gut.

Zum Erzeugen des kompletten RSS-Feeds nutze ich allerdings die Erweiterung [bolt-extension-rssfeed](https://github.com/bolt/bolt-extension-rssfeed "bolt-extension-rssfeed"). In dieser ist die URL dann allerdings wieder https://fryboyter.de/entries/Titel-des-Artikels. An sich kein Problem, da die Artikel mit und ohne /entries aufgerufen werden können. Wäre da nicht Isso Comment.

Isso Comment verknüpft die Kommentare und Artikel anhand des Titels. Und da ist der mit /entries eben ein andere als ohne. Ruft nun jemand einen Artikel über den globalen RSS-Feed auf und gibt einen Kommentar ab, wird die URL mit /entries in der Isso-Datenbank gespeichert. Da ich aber eben die Artikel dank des Routings ohne /entries veröffentliche tauchen die Kommentare somit auch nicht auf, so dass ich hier immer in der SQLite-Datenbank herumpfuschen muss. An sich kein Problem es nervt aber trotzdem.

Im Template für den RSS-Feed oben genannter Erweiterung gibt es folgende Codezeile.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-twig">&lt;link&gt;{{ url('contentlink', { 'contenttypeslug': record.contenttype.singular_slug, 'slug': record.slug } ) }}&lt;/link&gt;</code>
</pre>

In meinem nicht mehr ganz so jugendlichen Leichtsinn habe ich mir gedacht es reich hier einfach 'contenttypeslug': record.contenttype.singular_slug, zu entfernen. Pustekuchen. Sobald man versucht den Feed aufzurufen bekommt man eine unschöne Fehlermeldung. Zum einen reichen meine Programmierkenntnisse hier definitiv nicht aus, dass Problem zu lösen und zum anderen müsste ich nach jedem Update der Erweiterung diese anpassen. Also muss, zumindest vorübergehend, eine andere Lösung her.

Schlussendlich habe ich einfach die .htaccess-Datei für Bolt CMS angepasst. In dieser haben ich den Bereich &lt;IfModule mod_rewrite.c&gt; gesucht und in diesem folgende Zeile eingetragen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">RewriteRule ^entrie/(.+)$ https://fryboyter.de/$1 [R=301,L]</code>
</pre>

Abschließend noch den Cache von Bolt CMS gelöscht und fertig. Ruft nun jemand einen Link mit /entrie/ auf, wird er automatisch auf die Version ohne /entrie/ umgeleitet. Ich denke das ist derzeit die beste Lösung mit der ich nicht an der Erweiterung herumpfuschen muss.
