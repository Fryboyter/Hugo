---
title: Keepass Autotype unter LXDE
date: 2013-08-25T22:53:00+0100
categories:
- Linux
- OSBN
tags:
- Keepass
- Autotype
- LXDE
slug: keepass-autotype-unter-lxde
---
Zum verwalten einiger meiner Passwörter nutze ich das Programm [Keepass](http://keepass.info "KeePass"). Dieses Programm bietet unter anderem die Funktion dass man mittels Shortcut sich automatisch auf bestimmten Seiten anmelden kann, ohne Benutzername und das Passwort manuell aus dem entsprechenden KeePass-Eintrag kopieren zu müssen. Die Entwickler geben hierzu eine [Anleitung](http://keepass.info/help/v2/setup.html#mono "Keepass Anleitung Linux") für KDE, Gnome und Unity. Nur nutze ich auf dem Netbook LXDE. Und schon ist mal wieder Bastelstunde.

Um die globale Autotype-Funktion auch unter LXDE nutzen zu können, muss als erstes xdotools installiert werden. Als nächstes muss man dann den Shortcut anlegen, der die Autotype-Funktion ausführt. Hierzu muss man die Datei ~/.config/openbox/lxde-rc.xml öffnen und entsprechend bearbeiten. In der XML-Datei gibt es den Abschnitt . Innerhalb diesen Bereichs muss nun der Shortcut definiert werden. Am besten trägt man diesen vor ein, so dass man ihn bei Bedarf schnell wieder findet. Bei mir sieht der Eintrag wie folgt aus. Die letzte Zeile sollte bereits vorhanden sein.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">&lt;keybind key="C-A-y"&gt;
&lt;action name="Execute"&gt;
&lt;command&gt;keepass --auto-type&lt;/command&gt;
&lt;/action&gt;
&lt;/keybind&gt;
&lt;/keyboard&gt;</code>
</pre>

In der ersten Zeile definieren wir die Tastenkombination des Shortcuts. Das C steht hier für Strg, das A für ALT (genaueres kann man unter [http://openbox.org/wiki/Help:Bindings#Key_combination](http://openbox.org/wiki/Help:Bindings#Key_combination) nachlesen) und das y für y. Wer hier eine andere Kombination nehmen will, kann dies natürlich tun. In der zweiten Zeile wird angegeben, welche Aktion der Shortcut auslösen soll (genaueres unter [http://openbox.org/wiki/Help:Actions](http://openbox.org/wiki/Help:Actions)). In diesem Fall Execute, da ja ein Befehl ausgeführt werden soll. In der dritten Zeile wird dann der Befehl angegeben, der ausgeführt werden soll. Damit der Shortcut funktioniert, muss man sich aus- und wieder einloggen bzw. den Rechner neu starten. Nun sollte die Autotype-Funktion funktionieren, wenn die entsprechende KeePass-Datenbank geöffnet ist.
