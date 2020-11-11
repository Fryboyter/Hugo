---
title: DoFollow für Links
date: 2012-09-29T13:34:00+0100
categories:
- Allgemein
tags:
- Dofollow
- Wordpress
- Links
slug: dofollow-fuer-links
---
Da ich gerade etwas an dieser Wordpress-Installation gebastelt habe (deswegen auch der kurze Ausfall der Seite :D), habe ich gemerkt, dass Links in Kommentare auf nofollow gesetzt sind. Sprich Bots von Suchmaschinen verfolgen diese Links nicht. Zumindest wenn sie sich an nofollow halten. Ich habe dies nun geändert und das nofollow bei den Links entfernt. Dies funktioniert eigentlich recht einfach, indem man in der function.php des jeweiligen Child-Themes folgendes einträgt:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">function strip_nofollow($ret) {
$ret = str_replace("rel='external nofollow'","rel='external'", $ret);
return $ret;
add_filter('get_comment_author_link', 'strip_nofollow');</code>
</pre>

Ich behalte es mir natürlich vor, Links ggf. auf NoFollow zu setzen oder zu löschen. Das sollte aber eher die Ausnahme sein. Aber soviel "Hausrecht" nehme ich mir einfach heraus. Und das muss ich unter Umständen auch.