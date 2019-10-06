---
title: Manche Artikel werden nun mehrsprachig angeboten
date: 2019-05-18T14:19:00+0200
categories:
- OSBN
- Allgemein
tags:
- Fryboyter
- Hugo
- Mehrsprachigkeit
slug: manche-artikel-werden-nun-mehrsprachig-angeboten
---
In den letzten Jahren habe ich mir ab und zu überlegt, ob ich zumindest manche Artikel nicht zusätzlich auch auf Englisch veröffentliche. Bisher war mir allerdings die technische Umsetzung zu umständlich. Mit Hugo ist es allerdings schnell gemacht, wie ich heute festgestellt habe.

Als erstes erweitert man die Konfigurationsdatei config.toml um folgende Einträge.

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

Mit der ersten Zeile gibt man an, dass de die Standardsprache ist. Der Rest definiert die vorhandenen Sprachen, gibt Ihnen eine Bezeichnung und eine Gewichtung (umso niedriger umso wichtiger).

Nun erzeugt man einen neuen Artikel. Nennen wir die Datei einfach mal manche-artikel-nun-englisch.md. Nehmen wir nun einmal an, der Artikel ist wichtig genug, dass wir ihn nun auch auf Englisch veröffentlichen möchten. Also erzeugen wir einen weiteren Artikel und nennen die Datei manche-artikel-nun-englisch.en.md. Wie man sieht wurde der Titel um ein .en erweitert. Hugo kapiert nun automatisch, dass der Artikel mit .en die englische Version darstellt und die andere die deutsche Version.

Was aber, wenn nun jemand die deutschsprachige Version aufruft, aber kein Deutsch versteht? Hier müsste eine Art Umschalter vorhanden sein. Hierfür kann man zum Beispiel folgenden Code verwenden.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">{{ if .IsTranslated }}
	{{ range .Translations }} | &lt;a href=&quot;{{ .Permalink }}&quot;&gt;{{ .Language.LanguageName }}&lt;/a&gt; {{ end}}
{{ end }}
</code>
</pre>

Hiermit wird geprüft, ob der Artikel auch in einer anderen Sprache angeboten wird. Wenn ja wird auf die entsprechenden Versionen verlinkt. Wenn nicht, wird gar nichts angezeigt. Diesen Code habe ich auf fryboyter.de unter die Hauptüberschrift aller Artikel gepackt. Sollte dort nun bei einem Artikel der Link "English version" erscheinen, habe ich mir die Arbeit gemacht und den Artikel auch auf Englisch veröffentlicht. Aktuell wird man diese Verlinkung aber nur bei diesem Artikel finden. Nach und nach werden es aber mehr Artikel werden die ich auf Deutsch und Englisch anbiete (auch ältere).