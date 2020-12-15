---
title: Update auf Wallabag 2.4.0 - Row size to large
date: 2020-12-15T20:46:41+0100
categories:
- OSBN
- Allgemein
tags:
- Wallabag
- Mariadb
slug: wallabag-zeilenformat-zu-lang
---
Bei [Wallabag handelt](https://wallabag.org/en) es ich um ein Tool zum selbst hosten mit dem man interessante Internetseiten abspeichern kann um sie später zu lesen. Vor ein paar Tagen wurde Version 2.4.0 veröffentlicht auf die ich meine Instanz eben aktualisieren wollte.

Das Update ist leider mit der (gekürzten) Fehlermeldung "Syntax error or access violation: 1118 [Row size too large](https://mariadb.com/kb/en/innodb-row-formats-overview/#maximum-row-size)." abgebrochen und die Installation war nicht mehr nutzbar.

Die Ursache ist, dass in der Wallabag-Datenbank mindestens eine Tabelle das Zeilenformat "REDUNDANT" oder  "COMPACT" hat. Die betroffenen Tabellen kann man sich mit folgender Datenbankabfrage anzeigen.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-sql">SELECT CONCAT(TABLE_SCHEMA, '.', TABLE_NAME) 
FROM information_schema.TABLES 
WHERE ENGINE = 'InnoDB' AND ROW_FORMAT IN('Redundant', 'Compact') 
AND TABLE_NAME NOT IN('SYS_DATAFILES', 'SYS_FOREIGN', 'SYS_FOREIGN_COLS', 'SYS_TABLESPACES', 'SYS_VIRTUAL', 'SYS_ZIP_DICT', 'SYS_ZIP_DICT_COLS');</code>
</pre>

Da sich die Ausgabe nur auf ein paar Tabellen beschränkt hat und ich gerade keine Lust auf eine komplexere Lösung habe, habe ich bei diesen kurzerhand das Zeilenformat manuell mit folgendem Befehl auf "DYNAMIC" geändert.

<pre class="line-numbers language-sql" style="white-space:pre-wrap;">
<code class="language-sql">ALTER TABLE $TABLENAME ROW_FORMAT=DYNAMIC;</code>
</pre>

Anstelle von $TABLENAME trägt man eine der Tabellen ein die man mit der Datenbankabfrage angzeigt bekommen hat. 

Hat man die betreffenden Tabllen entsprechend geändert hat, sollte das Update ohne Fehler abschließen und die betreffende Wallabag-Instanz sollte danach nutzbar sein
