---
title: Wallabag auf Uberspace 7 installieren
date: 2018-04-29T23:44:00+0100
categories:
- Linux
- OSBN
tags:
- Wallabag
- Uberspace
slug: wallabag-auf-uberspace-7-installieren
---
Bei [Wallabag](https://wallabag.org/de) handelt es sich um eine Lösung zu selbst hosten mit der man interessante Internetseiten speichern kann um sie dann später zu lesen. Wallabag ist sozusagen eine Alternative zu Pocket das wohl die meisten Nutzer von Firefox kennen sollten.

Um Wallabag auf einen Uberspace 7 unter eine Subdomain zu installieren, kann man wie folgt vorgehen.

Als erstes erstellt man unter ~/html/ ein neues Verzeichnis (z. B. "walla") und welchseln in dieses. Nun führen wir folgenden Befehl aus um die nötigen Dateien für die Installation herunterzuladen.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">git clone https://github.com/wallabag/wallabag.git .</code>
</pre>

Der Punkt am Ende des Befehls ist übrigens kein Fehler sondern sorgt dafür, dass die Dateien im aktuellen Verzeichnis abgespeichert werden.

Wenn alles heruntergeladen ist, installiert man Wallabag mittels "make install". Das dauert ein Stück. Am Ende des Vorgangs beginnt ein Frage- und Antwortspiel bei dem zum Beispiel diverse Sachen wie die Datenbankverbindung usw. abgefragt werden. Hierbei gehe ich an dieser Stelle nur auf zwei Sachen ein, da der Rest eigentlich selbsterklärend ist. Das wäre zum einen "mailer_host". Hier ist der Standard 127.0.0.1. Daraus machen wir 127.0.0.1:587, da SMTP bei Uberspace auf Port 587 läuft. Bei "secret" sollte man anstelle des vorgegebenen Geheimnisses lieber ein eigenes eintragen.

Wenn wir die ganzen Informationen eingetragen bzw. abgenickt haben, erstellen wir nun noch im anfangs angelegten Verzeichnis eine .htaccess Datei mit folgenden Inhalt.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ /web/$1 [QSA,L]</code>
</pre>

Somit wir automatisch bei einem Aufruf in den Unterordnet web weitergeleitet.

Da wir in diesem Beispiel Wallabag ja unter einer Subdomain erreichbar machen wollen, sind nun noch folgende beide Befehle nötig.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">ln -s /var/www/virtual/$USER/html/walla /var/www/virtual/$USER/walla.domain.org\r\nuberspace\_web\_domain\_add\_walla.domain.org</code>
</pre>

Mit dem ersten Befehl wird der Symlink erstellt und mit dem zweiten wird die Subdomain bei Uberspace aktiviert. Anstelle von domain.org sollte man die eigene Domain angeben.

Das war es im Grunde genommen. Von nun an kann man Wallabag mittels walla.domain.org aufrufen und dort diverse Seiten abspeichern. Um das ganze etwas bequemer zu gestalten kann man sich noch die Browser-Erweiterung Wallabagger installieren. Diese ist für Firefox, Opera und Chrome bzw. Browser die darauf basieren erhältlich. Eine Anleitung zur Konfiguration findet man unter [https://wallabag.org/en/news/wallabagger-howto](https://wallabag.org/en/news/wallabagger-howto).
