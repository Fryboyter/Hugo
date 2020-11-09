---
title: Natürlich Wordpress - Oder doch nicht?
date: 2016-03-09T09:56:00+0100
categories:
- OSBN
- Allgemein
tags:
- Wordpress
- Standard
- Alternativen
slug: natuerlich-wordpress-oder-doch-nicht
---
Wordpress ist weit verbreitet. Wordpress hat eine große Gemeinschaft. Und Wordpress hat viele Plugins um den Funktionsumfang zu erweitern. Dennoch bin ich immer unzufriedener mit Wordpress. Es sind zwar nur Kleinigkeiten, aber trotzdem. Alle paar Tage gibt es Aktualisierungen für die Übersetzungen. Gefühlt wird hier jede Änderung in ein Update gepackt. Das Backend reagiert ab und zu recht träge, obwohl sich nichts geändert hat. Die Plugins sind auch so eine Sache. Manche sind unsicher, manche werden einfach nicht mehr betreut. Vor einigen Tagen bin ich dann auch noch so verrückt gewesen das Theme anzufassen.

Ich kann zwar etwas PHP, HTML, CSS, Python usw. aber als Programmierer würde ich mich nicht mal ansatzweise bezeichnen. Entweder ist genau das das Problem oder ich bin einfach zu unfähig. Womöglich beides. Auf jeden Fall endeten alle Versuche mein Theme anzupassen mehr oder weniger im Chaos. In der Hoffnung, dass es eine (für mich) bessere Lösung als Wordpress gibt, habe ich Google mal bis auf das Äußerste gequält. Und habe Bolt CMS gefunden. Das Ding ist ebenfalls ein Brocken wie Wordpress. Dennoch lässt sich das Backend jederzeit absolut flüssig aufrufen. Erstaunt hat mich dort zuerst einmal die Hauptkonfiguration. Klickt man auf diesen Punkt erscheint einfach eine Textdatei in einem Editor. Hätte ich jetzt nicht erwartet. Zumal der Rest über eine "richtige" grafische Oberfläche läuft. Diese ist Wordpress relativ ähnlich. Nach einigen kurzen Tests hat mich Bolt jetzt nicht absolut vom Hocker gehauen. Gefallen habe ich aber schon gefunden. Dann habe ich mich allerdings einmal an die Tempaltes gewagt. Hier wird [Twig](http://twig.sensiolabs.org "Twig") verwendet. Ich habe dann einfach mal versucht das von mir verwendete Theme von Wordpress nachzubauen. Nachdem ich die Funktionsweise von Twig verstanden hatte (was in dem Fall nicht mal wirklich lange gedauert hat), habe ich mir in weniger als einer Stunde ein fertiges Theme unter Bolt zusammengebaut. Und selbst ein paar Tage später verstehe ich noch, was in diesem passiert. Hier mal ein Beispiel für die Auflistung der einzelnen Artikel der Hauptseite:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-twig">{% include '_header.twig' %}
{% setcontent records = "entries/latest/5" allowpaging %}
    {% for record in records %}
        {{ record.title }}
        {{ record.body }}
        Veröffentlicht von {{ record.user.displayname }} am {{ record.datepublish|localdate("%d %B %Y") }}
    {% endfor %}
    {{ pager() }}
{% include '_aside.twig' %}
{% include '_footer.twig' %}</code>
</pre>

Das versteht man vermutlich schon fast, ohne das man jemals mit Twig gearbeitet hat. Keine Vergleich mit dem Wordpress-Wust. Man könnte es auch als idiotensicher bezeichnen. Also ideal für mich. :D

Leider hat Bolt CMS auch einen entscheidenden Nachteil für mich. Zumindest indirekt. Bolt verfügt als CMS nicht über eine Kommentarfunktion. Als Plugin gibt es zwar die eine oder andere Lösung. Von denen kommt allerdings nur [Isso Comments](https://posativ.org/isso "Isso Comments") in Frage, da man es selbst hosten kann, es einen Wordpress-Import gibt und es derzeit weiterentwickelt wird. Und genau da hakt es. Ich bekomme Isso auf meinem Uberspace ums Verrecken nicht zum Laufen. Der Entwickler hat leider keine, für mich, funktionierende Lösung parat. Und ich wüsste auch nicht, was ich bei der Installation falsch mache oder wie ich dem Entwickler helfen könnte. Das ist bestimmt wieder so ein Problem auf das man erst kommt, wenn man 2 Promille auf dem Tacho hat und sich den Baseballschläger bei Vollmond zweimal über die Rübe zieht während man nackt um ein Feuer tanzt. Sollte ich bezüglich Isso doch noch die Erleuchtung erfahren werde ich Wordpress Lebewohl sagen. Bis dahin geht es erst einmal mit Wordpress weiter. Es sind ja, wie schon gesagt, nur Kleinigkeiten die mich stören.