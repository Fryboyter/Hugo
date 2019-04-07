---
title: KDM Deutsch beibringen
date: 2010-07-11T18:15:00+0100
categories:
- Linux
- OSBN
tags:
- KDM
- Deutsch
slug: kdm-deutsch-beibringen
---
Seit einiger Zeit hatte ich das "Problem", dass die Oberfläche von KDM zwar deutsch war, aber das Tastaturlayout für die Eingabe des Benutzernamens und des Passworts in englisch. Das hat mich eigentlich nicht gestört, da ich des öfteren mit dem us_US Tastaturlayout arbeiten muss. Aber Sonntag ist Basteltag und ich habe KDM nun komplett eingedeutscht. War eigentlich ganz einfach. Man legt einfach unter /etc/X11/xorg.conf.d/ die Datei 20-keyboard.conf an und trägt dann folgendes ein:

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">Section "InputClass"
    Identifier "keyboard"
    MatchIsKeyboard "yes"
    Option "XkbLayout" "de"
    Option "XkbVariant" "nodeadkeys"
Endsection</code>
</pre>

Nun einfach den Rechner neu starten (den X-Server neu starten funktioniert vermutlich auch) und schwups, konnte ich mich wieder mit dem de_DE Tastaturlayout anmelden.
