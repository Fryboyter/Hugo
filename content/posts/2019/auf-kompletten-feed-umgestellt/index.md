---
title: "Auf Kompletten Feed Umgestellt"
date: 2019-04-27T18:07:22+02:00
categories:
- OSBN
- Allgemein
tags:
- Hugo
- Feed
slug: auf-kompletten-feed-umgestellt
---
Vor ein paar Tagen wurde ich gefragt, ob ich den OSBN-Feed nicht so ändern kann, dass dieser den kompletten Artikel anzeigt. Der Wunsch ist mir Befehl.

Hierzu habe ich einfach im Theme-Verzeichnis von Hugo im Unterverzeichnis layouts/_default die Datei rss.xml mit folgendem Inhalt angelegt (dieser entspricht dem Standard-Template des Feeds).

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">&lt;rss version=&quot;2.0&quot; xmlns:atom=&quot;http://www.w3.org/2005/Atom&quot;&gt;
  &lt;channel&gt;
    &lt;title&gt;{{ if eq  .Title  .Site.Title }}{{ .Site.Title }}{{ else }}{{ with .Title }}{{.}} on {{ end }}{{ .Site.Title }}{{ end }}&lt;/title&gt;
    &lt;link&gt;{{ .Permalink }}&lt;/link&gt;
    &lt;description&gt;Recent content {{ if ne  .Title  .Site.Title }}{{ with .Title }}in {{.}} {{ end }}{{ end }}on {{ .Site.Title }}&lt;/description&gt;
    &lt;generator&gt;Hugo -- gohugo.io&lt;/generator&gt;{{ with .Site.LanguageCode }}
    &lt;language&gt;{{.}}&lt;/language&gt;{{end}}{{ with .Site.Author.email }}
    &lt;managingEditor&gt;{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}&lt;/managingEditor&gt;{{end}}{{ with .Site.Author.email }}
    &lt;webMaster&gt;{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}&lt;/webMaster&gt;{{end}}{{ with .Site.Copyright }}
    &lt;copyright&gt;{{.}}&lt;/copyright&gt;{{end}}{{ if not .Date.IsZero }}
    &lt;lastBuildDate&gt;{{ .Date.Format &quot;Mon, 02 Jan 2006 15:04:05 -0700&quot; | safeHTML }}&lt;/lastBuildDate&gt;{{ end }}
    {{ with .OutputFormats.Get &quot;RSS&quot; }}
        {{ printf &quot;&lt;atom:link href=%q rel=\&quot;self\&quot; type=%q /&gt;&quot; .Permalink .MediaType | safeHTML }}
    {{ end }}
    {{ range .Pages }}
    &lt;item&gt;
      &lt;title&gt;{{ .Title }}&lt;/title&gt;
      &lt;link&gt;{{ .Permalink }}&lt;/link&gt;
      &lt;pubDate&gt;{{ .Date.Format &quot;Mon, 02 Jan 2006 15:04:05 -0700&quot; | safeHTML }}&lt;/pubDate&gt;
      {{ with .Site.Author.email }}&lt;author&gt;{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}&lt;/author&gt;{{end}}
      &lt;guid&gt;{{ .Permalink }}&lt;/guid&gt;
      &lt;description&gt;{{ .Summary | html }}&lt;/description&gt;
    &lt;/item&gt;
    {{ end }}
  &lt;/channel&gt;
&lt;/rss&gt;
</code>
</pre>

Damit nun der komplette Artikel angezeigt wird, habe ich die Zeile &lt;description&gt;{{ .Summary | html }}&lt;/description&gt; auf &lt;description&gt;{{ .Content | html }}&lt;/description&gt; geändert. Das war es schon. Die Änderung gilt für die komplette Seite und nicht nur für die Kategorie OSBN.