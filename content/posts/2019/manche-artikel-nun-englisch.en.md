---
title: Some articles are now offered in multiple languages
date: 2019-05-18T14:19:00+0200
categories:
- OSBN
- General
tags:
- Fryboyter
- Hugo
- Multilanguage
slug: some-articles-are-now-offered-in-multiple-languages
---
In the last few years I have been thinking about publishing at least some articles in English from time to time. So far, however, the technical implementation was too cumbersome for me. But with Hugo it's done pretty easy, as I noticed today.

The first thing to do is to add the following entries to the configuration file config.toml.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">DefaultContentLanguage = "de"

	[languages]
    [languages.de]
        languageName = "Deutsche Version"
        weight = 1
    [languages.en]
        languageName = "English version"
        weight = 2
</code>
</pre>

The first line specifies that de is the default language. The rest defines the existing languages, gives them a name and a weighting (the lower the more important).

Now we create a new article. Let's just call the file manche-artikel-nun-englisch.md. Let's assume that the article is important enough to be published in English as well. So we create another article and name the file manche-artikel-nun-englisch.en.md. As you can see the title has been extended by a .en. Hugo now automatically understands that the article with .en is the English version and the other one is the German version.

But what if someone opens the German version but doesn't understand German? There should be a kind of switch available. For this one can use for example the following code.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ if .IsTranslated }}
	{{ range .Translations }} | <a href="{{ .Permalink }}">{{ .Language.LanguageName }}</a> {{ end}}
{{ end }}
</code>
</pre>

This checks whether the article is also available in another language. If so, a link to the corresponding versions will be shown. If not, nothing is displayed. I put this code on fryboyter.de under the main heading of all articles. If the link "English version" appears at an article, I wrote the article in English as well. Currently one will find this link only at this article for the moment. Gradually there will be more articles in German and English (also older ones) available.