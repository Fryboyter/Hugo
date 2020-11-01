---
title: "Hugo - Inhalt aus Sitemap entfernen"
date: 2019-06-11T20:00:54+0200
categories:
- Allgemein
- OSBN
tags:
- Hugo
- Sitemap
slug: hugo-inhalt-aus-sitemap-entfernen
---
Google Search Console hat herumgemault, dass auf meiner Seite zwei Links durch die robots.txt gesperrt sind obwohl sie in der Sitemap auftauchen. Wie bekomme man diese nun aus der Sitemap heraus die Hugo automatisch erstellt?

Die Lösung ist eigentlich ganz einfach. Als erstes editiert man die betreffenden Artikel und erweitern die Metadaten um sitemap_exclude: true.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">---
title: Geheimer Artikel
date: 2019-06-11T19:12:45+0200
sitemap_exclude: true
slug: geheimer-artikel
---
</code>
</pre>

Nun muss noch das Template angepasst werden mit dem die Sitemap erzeugt wird. Hierfür erstellt man im Themeverzeichnis unter layouts/_default die Datei sitemap.xml und füllt diese mit folgendem Inhalt.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ printf &quot;&lt;?xml version=\&quot;1.0\&quot; encoding=\&quot;utf-8\&quot; standalone=\&quot;yes\&quot; ?&gt;&quot; | safeHTML }}
&lt;urlset xmlns=&quot;http://www.sitemaps.org/schemas/sitemap/0.9&quot;
  xmlns:xhtml=&quot;http://www.w3.org/1999/xhtml&quot;&gt;
  {{ range .Data.Pages }}
  &lt;url&gt;
    &lt;loc&gt;{{ .Permalink }}&lt;/loc&gt;{{ if not .Lastmod.IsZero }}
    &lt;lastmod&gt;{{ safeHTML ( .Lastmod.Format &quot;2006-01-02T15:04:05-07:00&quot; ) }}&lt;/lastmod&gt;{{ end }}{{ with .Sitemap.ChangeFreq }}
    &lt;changefreq&gt;{{ . }}&lt;/changefreq&gt;{{ end }}{{ if ge .Sitemap.Priority 0.0 }}
    &lt;priority&gt;{{ .Sitemap.Priority }}&lt;/priority&gt;{{ end }}{{ if .IsTranslated }}{{ range .Translations }}
    &lt;xhtml:link
                rel=&quot;alternate&quot;
                hreflang=&quot;{{ .Lang }}&quot;
                href=&quot;{{ .Permalink }}&quot;
                /&gt;{{ end }}
    &lt;xhtml:link
                rel=&quot;alternate&quot;
                hreflang=&quot;{{ .Lang }}&quot;
                href=&quot;{{ .Permalink }}&quot;
                /&gt;{{ end }}
  &lt;/url&gt;
  {{ end }}
&lt;/urlset&gt;
</code>
</pre>

Dies entspricht erst einmal dem Standard-Template für die Sitemap. Nun ändert man Zeile 4 wie folgt ab.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ range .Data.Pages }}{{ if ne .Params.sitemap_exclude true }}
</code>
</pre>

Abschließen erweitert man noch die Zeile 21 um ein weiteres {{ end }}.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ end }}{{ end }}
</code>
</pre>

Wird nun die Seite neu erzeugt sollten alle Inhalte bei denen sitemap_exclude: true hinterlegt wurde nicht mehr in der Sitemap erscheinen.