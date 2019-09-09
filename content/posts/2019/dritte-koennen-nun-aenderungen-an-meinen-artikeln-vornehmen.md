---
title: Dritte können nun Änderungen an meinen Artikeln vornehmen
date: 2019-09-08T20:55:14+0200
categories: 
- OSBN
- Allgemein
tags:
- Hugo
- Github
slug: dritte-koennen-nun-aenderungen-an-meinen-artikeln-vornehmen
---
Manchen Leuten ist scheinbar ab und zu sehr langweilig. Dieses Wochenende habe ich doch tatsächlich eine E-Mail mit Hinweisen auf den einen oder anderen Fehler in meinen Artikeln erhalten. Im Grunde waren es nur Rechtschreibfehler.

In der E-Mail wurde ich auf gefragt ob ich für solche Sachen nicht ein öffentlicht zugängliches Repository anbieten kann. Kann ich. Es ist unter [https://github.com/Fryboyter/Hugo](https://github.com/Fryboyter/Hugo) erreichbar.

Aber würde ich selbst einen Artikel lesen und dann das Repository aufrufen und die Datei suchen wen ich einen Fehler finden würde? Eher nicht. Daher habe ich nun einen Link unterhalb der jeweilige Artikelüberschrift eingebaut, der direkt auf die betreffende Datei bei Github verweist.

Als erstes habe ich hierfür in der Konfigurationsdatei von [Hugo](https://gohugo.io/) (config.toml) den Bereich [params] um einen Verweis auf das Repository eingetragen.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[params]
ghrepo = "https://github.com/Fryboyter/Hugo/"
</code>
</pre>

Als nächstes habe ich das verwendete Theme (single.html und list.html) von fryboter.de wie folgt erweitert.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">| &lt;a href=&quot;{{.Site.Params.ghrepo}}edit/master/content/{{.File.Path}}&quot; &gt;Bei Github bearbeiten&lt;/a&gt;
</code>
</pre>

Hiermit wird das in der Datei conifg.toml hinterlegte Verweis auf das Respository genutzt. Dieser wird dann einfachum edit/master/content/ erweitert, da sich dieser Teil nicht ändert. Ganz am Schluss wird mit {{.File.Path}} auf die betreffende Datei verlinkt.

Im Grunde ist das mal wieder ziemlich simpel. Huge gefällt mir immer mehr.