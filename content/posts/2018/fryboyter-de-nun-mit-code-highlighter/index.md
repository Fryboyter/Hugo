---
title: Fryboyter.de nun mit Code Highlighter
date: 2018-01-28T19:00:15+0100
categories:
- OSBN
- Allgemein
tags:
- Fryboyter
- Code Highlighter
- Prism
slug: fryboyter-de-nun-mit-code-highlighter
---
Vor ein paar Monaten bin ich von Wordpress auf Bolt CMS umgestiegen. Hierbei musste ich auf die eine oder andere Funktion verzichten. Unter anderem auf einen Code Higlighter. Es gibt zwar zwei Plugins, aber diese sind leider veraltet und funktionieren mit Bolt 3.x nicht und ich bekomme es nicht gebacken diese entsprechend anzupassen.

Daher hatte ich mit CSS etwas zusammengebastelt um Codebeispiele zumindest als solche zu kennzeichnen. Das Ergebnis war mehr schlecht als recht. Bei zu langen Zeilen musste man beispielsweise horizontal scrollen. Und Zeilennummern gab es auch keine mehr. Blöd wenn man den Code an einer bestimmten Stelle erklären will.

Ich habe mich daher dazu entschlossen einen Code Highlighter zu installieren. Entschieden habe ich mich schlussendlich für [Prism](http://prismjs.com). Zukünftig wird nun Code farblich hervorgehoben und Zeilennummern ink. Umbruch gibt es nun auch wieder.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash 
echo "Wie ist Ihr Name?"
read ANTWORT
if [ "$ANTWORT" == "root" ]
    then
        echo "Hallo, Administrator. Das ist eine sehr lange Zeile um einen Zeilenumbruch zu provozieren."
    else
        echo "Hallo, Anwender."
fi</code>
</pre>

Der ganze Spaß hat aber auch Nachteile. Zum einen muss ich nun einige Artikel anpassen, da ich oft zu faul war, die richtige Klasse bei den Code-Tags zu hinterlegen (z. B. &lt;code&gt; anstelle von &lt;code class="language-bash"&gt;. Und für die Zeilennummern muss ich die &lt;pre&gt; Tags um &lt;pre class="line-numbers" style="white-space:pre-wrap;"&gt; erweitern. Naja muss ich halt wieder das fleißige Bienchen spielen... Ein weiterer Nachteil ist, dass die Seite nun ca. 12 KB schwerer ist, da nun eine Javascript-Datei und eine CSS-Datei zusätzlich geladen werden. Ich denke das ist zu verkraften.