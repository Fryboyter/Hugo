---
title: Der Umzug auf Uberspace 7
date: 2018-01-02T15:11:00+0100
categories:
- Linux
- OSBN
tags:
- Umzug
- Uberspace
slug: der-umzug-auf-uberspace-7
---
Vor ein paar Wochen wurde Uberspace in Version 7 als Betaversion veröffentlicht. Eigentlich wollte ich zeitnah von version 6 umsteigen. Aus zwei Gründen habe ich den Umstieg aber erst einmal sein gelassen.

Grund 1: Es war noch nicht möglich mehrere E-Mail-Adressen anzulegen. Diese Funktion sollte und wurde auch nachgereicht. Wie gesagt, das ganze ist offiziell noch als Betaversion gekennzeichnet.

Grund 2: Das Team hinter Uberspace hat die Entscheidung getroffen, dass nur noch ein DocumentRoot pro Zugang möglich ist. Virtuelle DocumentRoots wird es nicht mehr geben. Auch wenn ich die Entscheidung aus technischer Sicht durchaus nachvollziehen kann, kommt für mich der Umstieg dann doch nicht in Frage, da ich mehrere Domains aufgeschaltet habe und im Falle von Fryboyter.de auch noch mehrere Dienste wie Searx unter Subdomains nutze. Aber egal, unter Version 6 funktioniert ja alles und wird wohl auch bis 2020 laufen.

Kurz vor Weihnachten hatte ich dann zufällig mal wieder bei Uberspace gestöbert und einen [Eintrag](https://blog.uberspace.de/die-sache-mit-den-virtuellen-documentroots) im Uberspace-Blog gefunden. Alleine das zeigt, dass man bei dem Anbieter gut aufgehoben ist. Andere Anbieter hätten eine Entscheidung getroffen und "friss oder stirb" wäre angesagt gewesen.

Da mir der aktuelle Stand von Uberspace 7 alles bietet, was ich aktuell so brauche, habe ich mir heute einmal einen Zugang besorgt. Auf die grundlegenden Sachen wie das erstellen des SSH-Zugang usw. gehe ich jetzt nicht ein. Das kann bei Bedarf unter https://manual.uberspace.de/en/index.html nachgelesen werden.

Allerdings nutze ich ja auch so spezielle Fälle wie Isso Comment. Ich kann mich an keine Installation erinnern bei der ich nicht irgendwo auf Granit gebissen bin. Heute hat es aber geklappt. Im Grunde habe ich mich an Martins [Anleitung](https://blog.posativ.org/2014/isso-und-uberspace-de) gehalten. Mit zwei Ausnahmen. Bei der Installation mit pip habe ich konservativ auf Version 2.7 gesetzt. Zudem bezieht sich die Anleitung auf das Ausführen per FastCGI. Aber auf meinem U7 gibt es (noch?) kein entsprechendes Verzeichnis. Allerdings wurde beim neuen Webspace daemontools von supervisord abgelöst. Also habe ich mir einfach folgenden Service gebastelt und Isso läuft.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">[program:isso]
command = /home/nutzer/.local/bin/isso -c /home/nutzer/etc/isso/user.cfg run
autostart = true
autorestart = true</code>
</pre>

Somit ist der restliche Umzug hoffentlich nur noch eine Fleißarbeit. Was sich allerdings wohl nicht vermeiden lässt ist, dass meine Seiten wohl vorübergehend nicht erreichbar sein werden, da ich z. b. für die Domains die A/AAAA und MX Records bei Inwx ändern muss. Also wenn die Seite fryboyter.de nicht erreichbar ist, ziehe ich entweder gerade um und/oder habe Mist gebaut.

<span style="color:#FF8C00;">**Es ist vollbracht. Der Wechsel von Uberspace V6 auf V7 hat ohne größere Probleme geklappt. Wer trotzdem noch einen Fehler findet oder Verbesserungswünsche hat, kann ich gerne melden.**</span>
