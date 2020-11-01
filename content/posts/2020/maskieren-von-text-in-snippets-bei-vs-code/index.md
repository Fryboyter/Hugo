---
title: Maskieren von Text in Snippets bei VSCode
date: 2020-01-03T17:45:23+0100
categories:
- OSBN
- General
tags:
- VSCode  
- Snippets
slug: maskieren-von-text-in-snippets-bei-vs-code
---
Urlaubszeit ist bei mir Bastelzeit. Daher bin ich gerade dabei mal wieder VSCode zu testen, obwohl ich mir vorab schon sicher bin, dass ich bei Sublime Text bleiben werde. Naja egal, darum geht es gerade nicht.

Damit ich relativ bequem Artikel veröffentlichen kann, habe ich mir unter Sublime Text diverse Snippets angelegt. Bei einem geht es darum, dass ich Text markiere und per Shortcut der HTML-Code hinzugefügt wird mit dem ich Text als Code hervorhebe. Somit wird zum Beispiel aus "10 PRINT "hallo welt" folgendes.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">&lt;pre class=&quot;line-numbers language-bash&quot; style=&quot;white-space:pre-wrap;&quot;&gt;
&lt;code class=&quot;language-bash&quot;&gt;10 PRINT &quot;hallo welt&quot;&lt;/code&gt;
&lt;/pre&gt;</code>
</pre>

Unter VSCode habe ich mir folgendes Snippet angelegt.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">&quot;wrap_highlight&quot;: {
&#x9;&#x9;&quot;prefix&quot;: &quot;wrap_highlight&quot;,
&#x9;&#x9;&quot;body&quot;: [
&#x9;&#x9;&#x9;&quot;&lt;pre class=&quot;line-numbers language-bash&quot; style=&quot;white-space:pre-wrap;&quot;&gt;&quot;,
&#x9;&#x9;&#x9;&quot;&lt;code class=&quot;language-bash&quot;&gt;$TM_SELECTED_TEXT&lt;/code&gt;&quot;,
&#x9;&#x9;&#x9;&quot;&lt;/pre&gt;&quot;
&#x9;&#x9;],
&#x9;&#x9;&quot;description&quot;: &quot;Highlight Code&quot;
&#x9;},</code>
</pre>

Sieht eigentlich ganz gut aus, macht aber nicht was es soll. Denn als Ausgabe erhält man folgendes.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">&lt;pre class=
 style=
&lt;code class=
&gt;10 PRINT &quot;hallo welt&quot;&lt;/code&gt;
&lt;/pre&gt;</code>
</pre>

Die Lösung ist in dem Fall allerdings recht einfach. Die Ursache ist die fehlende Maskierung (auch escapen genannt) der Anführungszeichen innerhalb des Bereichs "body". 

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">&quot;wrap_highlight&quot;: {
&#x9;&#x9;&quot;prefix&quot;: &quot;wrap_highlight&quot;,
&#x9;&#x9;&quot;body&quot;: [
&#x9;&#x9;&#x9;&quot;&lt;pre class=\&quot;line-numbers language-bash\&quot; style=\&quot;white-space:pre-wrap;\&quot;&gt;&quot;,
&#x9;&#x9;&#x9;&quot;&lt;code class=\&quot;language-bash\&quot;&gt;$TM_SELECTED_TEXT&lt;/code&gt;&quot;,
&#x9;&#x9;&#x9;&quot;&lt;/pre&gt;&quot;
&#x9;&#x9;],
&#x9;&#x9;&quot;description&quot;: &quot;Highlight Code&quot;
&#x9;},
</code>
</pre>

Ändert man das Snippet wie oben angegeben macht es auch das was es soll.