---
title: Nachbesserungen an Bolt CMS
date: 2017-06-27T15:01:00+0100
categories:
- OSBN
- Allgemein
tags:
- Fryboyter
- Änderungen
- Bolt CMS
slug: nachbesserungen-an-bolt-cms
---
Eigentlich war es mir schon klar, dass der Umstieg nicht so klappt wie erhofft. Bisher sind es aber nur ein paar Kleinigkeiten die schnell behoben werden konnten.

Zum einen stand in der PHP-Datei die den OSBN-Feed erstellt noch die Testdomain auf der ich die ganze Zeit an Bolt gebastelt habe. Somit hat gestern der Artikel von mir auf osbn nicht auf fryboyter.de sondern planetlinux.de verlinkt. Mea culpa. Hier habe ich zum einen die PHP-Datei geändert und zum anderen eine 301-Weiterleitung per .htaccess eingerichtet.

Das zweite Problem war mir anfangs nicht ganz klar. Ein Leser von fryboyter.de hat mir mitgeteilt, dass er keine Artikel direkt aufrufen kann, sondern nur die Hauptseite. Schnell bin ich auf die Fehlermeldung "Impossible to access an attribute ("id") on a null variable" gestoßen die sich auf die Datei record.twig bezieht die für die Anzeige einzelner Artikel zuständig ist. Dort gibt es unter anderem folgenden Code.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-twig">{% if user.id == 'X' %}
| &lt;a href="{{ paths.bolt }}editcontent/entries/{{ record.id }}"&gt;Bearbeiten&lt;/a&gt;
{% endif %}</code>
</pre>

Hiermit wird geprüft, ob der Nutzer der die Seite aufruft die Id X hat. Wenn ja, wird ein Link angezeigt mit dem man den Aritkel bearbeiten kann. Und genau wegen diesem Code knallt es. Aber warum?

In der Hauptkonfiguration von Bolt gibt es folgenden Bereich...

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-twig"># Use strict variables. This will make Bolt complain if you use {{ foo }},
# when foo doesn't exist.\
strict_variables: false</code>
</pre>

Tja hier hatte ich wohl das false auf true geändert um leere bzw. nicht vorhandene Variablen zu unterbinden. Und genau das ist die Ursache des Problems. Anstelle aus dem true wieder ein false zu machen, habe ich einfach obigen Code so abgeändert, dass erst einmal geprüft wird ob user.id definiert ist. Wenn ja, erfolgt die Prüfung auf ID X und wenn nicht, passiert gar nichts.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-twig">{% if user.id is defined %}
{% if user.id == 'X' %}
| &lt;a href="{{ paths.bolt }}editcontent/entries/{{ record.id }}"&gt;Bearbeiten&lt;/a&gt;
{% endif %}
{% endif %}
</code>
</pre>