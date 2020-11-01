---
title: "Hugo - Remove content from sitemap"
date: 2019-06-11T20:00:54+0200
categories:
- General
- OSBN
tags:
- Hugo
- Sitemap
slug: remove-content-from-sitemap
---
Google Search Console has complained that two links on my site are blocked by robots.txt even though they appear in the sitemap. How do I get them from the sitemap that Hugo creates automatically?

The solution is actually quite simple. First edit the related articles and add sitemap_exclude: true to the metadata.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">---
title: Secret Article
date: 2019-06-11T19:12:45+0200
sitemap_exclude: true
slug: secret-article
---
</code>
</pre>

Now it is necessary to adapt the template with which the sitemap is created. Therefore create the file sitemap.xml in the theme directory under layouts/_default and fill it with the following content.

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

This corresponds initially to the standard template for the sitemap. Now change line 4 as follows.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ range .Data.Pages }}{{ if ne .Params.sitemap_exclude true }}
</code>
</pre>

Finally add another {{ end }} to line 21.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ end }}{{ end }}
</code>
</pre>

If the page is rebuilt now, all contents where sitemap_exclude: true is specified should no longer appear in the sitemap.