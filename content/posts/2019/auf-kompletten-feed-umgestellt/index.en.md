---
title: Switched to Complete Feed
date: 2019-04-27T18:07:22+02:00
categories:
- OSBN
- General
tags:
- Hugo
- Feed
slug: switched-to-complete-feed
---
A few days ago I was asked if I could change the OSBN feed to show the complete article. The wish is my command.

To do this, I simply created the file rss.xml in the layouts/_default subdirectory of Hugo's theme directory with the following content (this corresponds to the standard template of the feed).

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

I changed the line &lt;description&gt;{ .Summary | html }}&lt;/description&gt; to &lt;description&gt;{ .Content | html }}&lt;/description&gt; to display the complete article. That's it. The change applies to the entire page, not just the OSBN category.