---
title: Htaccess, RewriteCond und RewriteRule. Oder wie treibt man mich in den Wahnsinn
date: 2011-03-01T09:17:00+0100
categories:
- OSBN
- Allgemein
tags:
- Htaccess
- RewriteCond
- RewriteRule
- Umleiten
slug: htaccess-rewritecond-und-rewriterule-oder-wie-treibt-man-mich-in-den-wahnsinn
---
Ich hatte am vergangenen Wochenende einige Sachen im Board umgestellt. Soweit ja kein Problem. Nur hat nun der Link der bei Google auf meine TrueCrypt-FAQ gezeigt hat (http://www.operation-tunnelbau.de/index.php?topic=27.0), nicht mehr gepasst. Diesen wollte ich nun auf das Wiki umleiten. Und was soll ich sagen? Ich hasse Htaccess, RewriteCond und RewriteRule. Naja eigentlich bin ich vermutlich einfach zu blöd dazu. Hier nun des Rätsels Lösung. Vielleicht hilft das den einen oder anderen ja weiter.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">RewriteCond %{SCRIPT_FILENAME} index.php 
RewriteCond %{QUERY_STRING} topic=27\\.0
RewriteRule ^(.*)$ http://www.wiki.operation-tunnelbau.de? [L,R=301]</code>
</pre>

Im Grunde eigentlich nicht schwer und Gott sei Dank ohne kompliziertes Regex. Sonst wäre es komplett vorbei gewesen.