---
title: IP-Nummer in der Isso-Datenbank nach 7 Tagen anonymisieren
date: 2020-02-18T10:13:19+0100
categories:
- OSBN
- General
tags:
- Isso  
- IP-Nummern
slug: ip-nummer-in-der-isso-datenbank-nach-7-tagen-anonymisieren
---
Martin von blog.mdosch.de hat vor einiger Zeit einen [Artikel](https://blog.mdosch.de/2018/05/20/isso-ip-adressen-woechentlich-loeschen/) veröffentlicht in dem er gezeigt hat, wie man die in der Datenbank von [Isso](https://github.com/posativ/isso) gespeicherten IP-Nummern der Kommentare anonymisiert indem man diese einmal wöchentlich mit 127.0.0.1 überschreibt.

Den Befehl (Update comments set remote_addr = "127.0.0.1";) habe ich damals für meine Isso-Instanz übernommen. Am Wochenende hatte ich mir mal wieder meine diversen Konfigurationen und Dokumentationen angesehen und bin auch auf besagten Befehl gestoßen. Hierbei habe ich mir überlegt, was ist wenn jemand die IP-Nummer jedes einzelnen Eintrags für beispielsweise 7 Tage aufbewahren will oder muss? Denn das klappt mit dem Befehl nicht wirklich.

Denn nehmen wir mal an, der Cronjob der den Befehl ausführt wird immer am Sonntag um 15 Uhr gestartet. Schreibe nun jemand um 14 Uhr einen Kommentar wird dessen IP-Nummer in der Datenbank trotzdem um 15 Uhr mit 127.0.0.1 überschrieben.

Ich habe mir daher einmal die Datenbank von Isso genauer angesehen. In der Tabelle comments gibt es die Spalte created. In dieser ist pro Kommentar ein Wert wie 1369140347.0 vorhanden. Hierbei handelt es sich um die sogenannte [Unixzeit](https://de.wikipedia.org/wiki/Unixzeit) die angibt wie viele Sekunden seit dem 01. Januar 1970, 00:00 UTC vergangen sind. Die Verwendung dieser Zeitrechnung ist in Datenbanken weit verbreitet, aber für den Menschen quasi nicht lesbar und nicht im Kopf umrechenbar.

Ich habe mir daher erst einmal eine Ausgabe erstellt die mir den Timestamp, den Timestamp in einer für Menschen lesbaren Forum sowie den jeweiligen Kommentar anzeigt.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-bash">SELECT created, strftime('%d-%m-%Y %H:%M:%f', datetime(created, 'unixepoch')) as createdhr, text 
FROM comments;
</code>
</pre>

Somit sehe ich bei weiteren Tests wie alt die Kommentare tatsächlich sind.

Als nächstes habe ich den Befehl so erweitert, dass nur die Kommentare angezeigt werden, die 7 Tage alt sind.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-bash">SELECT created, strftime('%d-%m-%Y %H:%M:%f', datetime(created, 'unixepoch')) as createdhr, text 
FROM comments
WHERE created > strftime("%s", "now", "-7 days");
</code>
</pre>

Hiermit wird der aktuelle Zeitpunkt abzüglich 7 Tage berechnet und verglichen ob der Wert in created größer als dieser Wert ist.

Hierbei werden allerdings auch die Kommentare angezeigt bei denen die IP-Adresse in der Spalte remote_addr bereits auf 127.0.0.1 geändert wurde. Da es unnötig ist jedes mal den Wert mit dem gleichen Wert zu überschreiben, habe ich den Befehl nun noch einmal um eine Bedingung erweitert bei der nur die Einträge angezeigt werden bei denen bei remote_address etwas anderes als 127.0.0.1 eingetragen ist.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-bash">SELECT created, strftime('%d-%m-%Y %H:%M:%f', datetime(created, 'unixepoch')) as createdhr, text 
FROM comments
WHERE created > strftime("%s", "now", "-7 days")
AND NOT remote_addr = '127.0.0.1';
</code>
</pre>

Nachdem ich mir nach ein paar Tests ziemlich sicher bin, dass es funktioniert habe ich den Befehl so geändert, dass er mir die betreffenden Einträge nicht anzeigt sondern bei diesen die IP-Nummern mit 127.0.0.1 überschreibt.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-bash">Update comments set remote_addr = "127.0.0.1"
WHERE created > strftime("%s", "now", "-7 days")
AND NOT remote_addr = '127.0.0.1';
</code>
</pre>

Nun kann man den Befehl mittels eines Cronjobs täglich ausführen. Hierbei sollte man allerdings berücksichtigen, dass die Berechnung des Alters nicht absolut genau ist, so das manche Kommentare unter Umständen erst nach 7,x der 8 Tagen berücksichtigt werden. Hier dürfte es helfen den Cronjob so zu konfigurieren, dass er mehrmals pro Tag ausgeführt wird. Wer in seiner Datenbank noch Einträge mit einer richtigen IP-Nummer hat die älter als 7 Tage sind, sollte den Befehl einmalig manuell ausführen und anstelle von "-7 days" einen entsprechend höheren Wert eintragen so dass alle Kommentare berücksichtigt werden.

Wer sich genauer informieren will, was zum Beispiel strftime oder datetime genau macht, kann dies zum Beispiel unter [https://www.sqlite.org/lang_datefunc.html](https://www.sqlite.org/lang_datefunc.html) tun.