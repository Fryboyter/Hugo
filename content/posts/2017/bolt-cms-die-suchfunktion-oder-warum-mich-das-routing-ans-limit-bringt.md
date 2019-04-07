---
title: Bolt CMS - Die Suchfunktion oder warum mich das Routing ans Limit bringt
date: 2017-06-05T13:16:00+0100
categories:
- OSBN
tags:
- Fryboyter
- Bolt CMS
- Routing
slug: bolt-cms-die-suchfunktion-oder-warum-mich-das-routing-ans-limit-bringt
---
Die Umstellung von fryboter.de von Wordpress auf Bolt CMS verkommt langsam einer unendlichen Geschichte. Kaum bin ich \"fertig\", kommt mir eine neue Idee, was ich noch ändern kann. Wichtig war mir aber schon immer die Suchfunktion.

Schon seit ich mir der Umstellung begonnen habe, hat es mich gestört, dass die Suchfunktion bei Bolt nicht funktioniert hat. Das Suchfeld einzubauen war eigentlich kein Problem. Aber bei jeder Suche bekam ich einen Fehler 404 angezeigt. Die Lösung des Problems zeigt mal wieder, dass auch Bolt CMS Ecken und Kanten hat. Wobei man hier nicht von einem Fehler an sich reden kann, sondern davon, dass Bolt CMS einige Stellschrauben hat.

So würde die Grundinstallation beispielsweise auf einen Artikel in Form von https://planetlinux.de/entrie/deutschsprachiger-usenet-server-mit-schwerpunkt-arch-linux verlinken. Da aber Google die Artikel in Form von https://planetlinux.de/deutschsprachiger-usenet-server-mit-schwerpunkt-arch-linux indexiert hat, ist das blöd, weil ich nicht von null anfangen oder mit htaccess tricksen will.

Hier kommt nun der Teil von Bolt CMS ins Spiel der mir immer noch Kopfschmerzen bereitet. Das [Routing](https://docs.bolt.cm/3.3/configuration/routing#). Hiermit lassen sich kurz gesagt die Aufrufe umbiegen. Um das "entrie/" aus den Artikellinks zu entfernen habe ich folgendes als erstes in die Datei routing.yml eintragen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-yaml">pagebinding:
path: /{slug}
defaults:
   _controller: controller.frontend:record
   contenttypeslug: entrie
   contenttype: entriest;</code></pre>


Als erstes weil die Einträge ganz oben die höchste Priorität haben. Um so weiter unten Sie in der Datei stehen um so weniger Priorität haben sie (und werden somit zum Beispiel nicht beachtet). Das Beispiel zeigt zum Beispiel dass alle Inhalte mit dem Inhaltstyp entries über den Pfad /slug ereichbar sind. Also zum Beispiel https://planetlinux.de/deutschsprachiger-usenet-server-mit-schwerpunkt-arch-linux.

Ein Stückchen weiter unten in der Datei ist bereits die Route für die Suche vorhanden.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-yaml">search: path: /search defaults: _controller: controller.frontend:search</code></pre>

Aber egal was ich versucht habe, die Suche hat immer nur den Fehler 404 ausgespuckt. Eine Zeit lang war ich soweit, dass es zukünftig einfach keine Suchfunktion geben wird. Punkt. Ende. Aus. Die Lösung war dann doch recht "einfach". So richtig kapiere ich sie aber trotzdem nicht. Ich habe einfach den Teil mit der sich auf die Suche bezieht über den Teil mit dem Pagebinding eingetragen. Und schon funktioniert die Suchfunktion. Klar es hat etwas mit der Priorität zu tun. Aber /search und /{slug} sind doch zwei unterschiedliche Sachen, oder nicht? Naja das ist erst mal egal. Es funktioniert ja.

Was jetzt noch fehlt ist der RSS-Feed für eine bestimmte Kategorie. Irgendwie muss ich ja meine Artikel auf osbn.de veröffentlichen. Es gibt zwar eine [Erweiterung](https://github.com/bolt/bolt-extension-rssfeed) aber diese kann "nur" einen seitenweiten Feed bzw. einen pro Inhaltstyp erstellen. Und der Inhaltstyp umfasst alle Artikel die ich auf fryboyter.de veröffentliche. Da hier auch mal der eine oder andere Artikel veröffentlicht wird, der nichts mit osbn.de zu tun hat ist das blöd... Noch blöder ist es, dass ich absolut keine Ahnung habe wie ich diese Erweiterung ändern könnte.

Ich habe daher einfach mal den Entwickler der Erweiterung auf Github gefragt, ob eventuell in absehbarer Zeit auch Feeds für einzelnen Kategorien möglich sein werden. Bisher habe ich aber noch keine Antwort erhalten. Zur Not habe ich mir auch einfach mal eine PHP-Datei gezaubert die mir einen Feed erstellt. Besonders froh bin ich aber nicht mit der Lösung. Wer will, kann sie sich ja mal ansehen...

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-php">echo '&lt;'.'?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?'.'&gt;'; ?&gt; 
&lt;rss version=&quot;2.0&quot;
    xmlns:content=&quot;http://purl.org/rss/1.0/modules/content/&quot;
    xmlns:wfw=&quot;http://wellformedweb.org/CommentAPI/&quot;
    xmlns:dc=&quot;http://purl.org/dc/elements/1.1/&quot;
    xmlns:atom=&quot;http://www.w3.org/2005/Atom&quot;
    xmlns:sy=&quot;http://purl.org/rss/1.0/modules/syndication/&quot;
    xmlns:slash=&quot;http://purl.org/rss/1.0/modules/slash/&quot;
    &gt;

&lt;channel&gt;
    &lt;title&gt;Fryboyter.de&lt;/title&gt;
    &lt;atom:link href=&quot;https://fryboyter.de/files/feed.xml&quot; rel=&quot;self&quot; type=&quot;application/rss+xml&quot; /&gt;
    &lt;description&gt;&lt;/description&gt;
    &lt;language&gt;de-DE&lt;/language&gt;
    &lt;link&gt;https://fryboyter.de&lt;/link&gt;    
    &lt;sy:updatePeriod&gt;hourly&lt;/sy:updatePeriod&gt;
    &lt;sy:updateFrequency&gt;1&lt;/sy:updateFrequency&gt;

&lt;?php 

$host = &quot;localhost&quot;;
$user = &quot;Nutzer&quot;;
$pass = &quot;Passwort&quot;;
$dbase = &quot;Datenbankname&quot;;

$connection = mysqli_connect(&quot;$host&quot; , &quot;$user&quot; , &quot;$pass&quot;) OR DIE (&quot;Keine Verbindung zu der Datenbank moeglich.&quot;);
mysqli_select_db($connection , $dbase) or die (&quot;Auswahl der Datenbank nicht moeglich.&quot;);

// Datenbankabfrage
$query = &quot;SELECT bolt_entries.slug AS slug, bolt_entries.datepublish AS date, bolt_entries.title AS title, bolt_entries.body AS blabla FROM bolt_entries, bolt_taxonomy WHERE bolt_entries.id = bolt_taxonomy.content_id AND bolt_taxonomy.slug = 'osbn' AND bolt_entries.status = 'published' ORDER BY bolt_entries.datepublish DESC LIMIT 20&quot;;  
$result = mysqli_query($connection , $query) or die (mysql_error()); 

// Ausgabe der Daten
while ($row = mysqli_fetch_array($result)){ 
    $slug = $row['slug']; 
    $title = $row['title']; 
    $blabla = $row['blabla']; 
    $pubdate = strtotime($row['date']);
    $pubdate = date('r', $pubdate);     
?&gt; 
    &lt;item&gt;
        &lt;title&gt;&lt;?php echo $title; ?&gt;&lt;/title&gt;
        &lt;link&gt;https://planetlinux.de/&lt;?php echo $slug; ?&gt;&lt;/link&gt;
           &lt;guid isPermaLink=&quot;false&quot;&gt;https://fryboyter.de/&lt;?php echo $slug; ?&gt;&lt;/guid&gt;
        &lt;pubDate&gt;&lt;?php echo $pubdate; ?&gt;&lt;/pubDate&gt;
        &lt;description&gt;&lt;![CDATA[&lt;?php echo $blabla; ?&gt;]]&gt;&lt;/description&gt;
    &lt;/item&gt;
&lt;?php } /* close while*/ ?&gt;

&lt;/channel&gt;
&lt;/rss&gt;
</code>
</pre>

Die Ausgabe der Datei in eine XML-Datei weitergeleitet erzeugt zumindest schon mal einen validen Feed. Allerdings müsste ich die Datei per Cronjob laufen lassen. Auf eine Lösung wie die Datei aufgerufen wird, sobald ein neuer Artikel veröffentlicht wurde, bin ich noch nicht gekommen.