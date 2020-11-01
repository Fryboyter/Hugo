---
title: Kommentarfunktion Isso unter Hugo deaktivieren
date: 2019-07-06T20:12:06+0200
categories:
- OSBN
- Allgemein
tags:
- Hugo
- Isso
- Kommentarfunktion
slug: kommentarfunktion-isso-unter-hugo-deaktivieren
---
Ein Bekannter von mir nutzt für seine Internetseite ein selbst (schlecht) programmierte Lösung. Er hat sich nun selbst für eine Kombination aus [Hugo](https://gohugo.io/) und [Isso](https://github.com/posativ/isso) entschieden. Allerdings stört es ihn, dass man die Kommentarfunktion nicht deaktivieren kann. 

Daher hat er mich nach einer Alternative für Isso gefragt. Da ich aber keine Erfahrungen mit anderen Kommentarfunktionen habe, habe ich mir überlegt, wie man Isso trotzdem für einzelne Artikel deaktivieren kann. Was leichter als gedacht ist.

Isso bindet man normalerweise wie folgt ein.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">&lt;section id=&quot;isso-thread&quot; data-title=&quot;Fryboyter.de um Suchfunktion erweitert&quot;&gt;&lt;/section&gt;
&lt;noscript&gt;&lt;p&gt;Die Kommentarfunktion kann nur mit aktiviertem Javascript genutzt werden&lt;/p&gt;&lt;/noscript&gt;
</code>
</pre>

Damit wird die Eingabemaske aber immer angezeigt. Wie kann man also verhindern, dass diese bei bestimmten Artikeln nicht angezeigt wird? Die Lösung ist bei Hugo if else.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ if ne .Params.nocomments true }}
&lt;section id=&quot;isso-thread&quot; data-title=&quot;{{ .Title }}&quot;&gt;&lt;/section&gt;
&lt;noscript&gt;&lt;p&gt;Die Kommentarfunktion kann nur mit aktiviertem Javascript genutzt werden&lt;/p&gt;&lt;/noscript&gt;
{{ else }}
&lt;p&gt;Die Kommentarfunktion ist f&uuml;r diesen Artikel deaktiviert&lt;/p&gt;
{{ end }}
</code>
</pre>

Hiermit wird geprüft, ob nocomments nicht true ist. Wenn ja, wird die Eingabemaske von Isso angezeigt. Ist nocomments allerdings true, wird der Hinweis angezeigt, dass die Kommentarfunktion deaktiviert ist.

Soll nun bei einem bestimmten Artikel die Kommentarfunktion deaktiviert werden, erweitert man den Frontmatter-Bereich einfach entsprechend.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">---
title: Kommentarfunktion Isso unter Hugo deaktivieren
date: 2019-07-06T20:12:06+0200
categories:
- OSBN
- Allgemein
tags:
- Hugo
- Isso
- Kommentarfunktion
nocomments: true
slug: kommentarfunktion-isso-unter-hugo-deaktivieren
---
Ein Bekannter von mir nutzt für seine Internetseite ein selbst (schlecht) programmierte Lösung. Er hat sich nun selbst...
</code>
</pre>

Das war es auch schon. Was man auch noch machen könnte, wäre anhand von nocomments: true zu prüfen ob die Javascript-Datei von Isso überhaupt geladen werden soll oder nicht.